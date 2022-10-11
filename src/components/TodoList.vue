<template>
    <div class=""> 
      <TodoListItem
        v-for="item in items"
        :key="item.id"
        :item="item"
        @edit="handleEdit"
        @delete="handleDelete"
      />
    </div>
  </template>
  
  <script>
  import TodoListItem from "./TodoListItem.vue";
  
  export default {
    components: {
      TodoListItem,
    },
      props: {
        items: {
          type: Array,
          required: true,
      },
    },
  
    setup(_, { emit }) {            // e 'emit'
      function handleEdit(item) {
        emit("edit", item);       //aplicar edição
      }
  
      function handleDelete(item) {
        emit("delete", item);        
      }
  
      return {
        handleEdit,
        handleDelete,
      };
    },
  };
  </script>