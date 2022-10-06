<template>
    <div class="font-sans font-light space-y-4">
      <div>
        <h1 class="font-sans font-semi-bold text-center pb-10 text-4xl text-black">Minha Lista</h1>
      </div>
      <div>
        <TodoForm :item="item" @save="handleSave" />
      </div>
      <div>
        <TodoList :items="items" @edit="handleEdit" @delete="handleDelete" />
      </div>
    </div>
  </template>
  
  <script>
  import { ref, watch } from "vue";
  import TodoForm from "./TodoForm.vue";
  import TodoList from "./TodoList.vue";
  
  function newItem() {
    return {
      id: null,
      text: "",
      timestamp: null,
    };
  }
  
  function getItemsFromStorage() {
    try {
      return JSON.parse(localStorage.getItem("items")) || [];
    } catch (e) {
      return [];
    }
  }
  
  function saveItemsToStarage(items) {
    try {
      localStorage.setItem("items", JSON.stringify(items));
    } catch (e) {
      
    }
  }
  
  export default {
    components: {
      TodoForm,
      TodoList,
    },
  
    setup() {
      const item = ref(newItem());
      const items = ref(getItemsFromStorage());
  
      watch(
        () => items,
        () => saveItemsToStarage(items.value),
        { deep: true }
      );
  
      function findItemIndex(itemToFindIndex) {
        return items.value.findIndex((item) => item.id === itemToFindIndex.id);
      }
  
      function addNewItem(item) {
        items.value.push({
          ...item,
          id: new Date().getTime(), // use timestamp as ID
          timestamp: new Date().getTime(),
        });
      }
  
      function deleteItem(item) {
        items.value.splice(findItemIndex(item), 1);
      }
  
      function updateExistingItem(item) {
        items.value.splice(findItemIndex(item), 1, item);
      }
  
      function handleSave(itemToSave) {
        if (itemToSave.id) {
          updateExistingItem(itemToSave);
        } else {
          addNewItem(itemToSave);
        }
  
        item.value = newItem();
      }
  
      function handleEdit(itemToEdit) {
        item.value = itemToEdit;
      }
  
      function handleDelete(itemToDelete) {
        deleteItem(itemToDelete);
      }
  
      return {
        item,
        items,
        handleSave,
        handleEdit,
        handleDelete,
      };
    },
  };
  </script>