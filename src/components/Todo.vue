<template>
    <div class="font-sans font-thin space-y-4" >
      <div>
        <h1 class="font-sans font-light text-center pb-6 text-4xl text-slate-800">Minhas tarefas</h1>
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
  
  function getItemsFromStorage() {  //colocar itens na memória
    try {
      return JSON.parse(localStorage.getItem("items")) || [];
    } catch (e) {
      return [];
    }
  }
  
  function saveItemsToStarage(items) { //salvar
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
          id: new Date().getTime(), //e timestamp e 'Id' s
          timestamp: new Date().getTime(),
        });
      }
  
      function deleteItem(item) {                       //deletar
        items.value.splice(findItemIndex(item), 1);
      }
  
      function updateExistingItem(item) {                //atualizar item
        items.value.splice(findItemIndex(item), 1, item);
      }
  
      function handleSave(itemToSave) {  //salvar novo item
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
        deleteItem(itemToDelete);                //deletar
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