<template>
    <div class=" shadow space-y-2">
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
  
    setup(_, { emit }) {
      function handleEdit(item) {
        emit("edit", item);
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