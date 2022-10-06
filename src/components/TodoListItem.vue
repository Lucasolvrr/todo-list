<template>
    <div class="flex flex-wrap items-center shadow my-5 py-2 pr-4 pb-2 text-bold">

      <div class=" pr-2 font-normal rounded-3xl rounded-l-lg  ml-4 text-bold">
        {{ item.text }}
      </div>
      <div class="ml-auto space-x-2">
        <button
          type="button"
          class="appearance-none bg-green-500 rounded text-white px-3 py-1 text-xs focus:outline-none focus:ring hover:bg-green-600"
          @click="handleEditClick"
        >
          editar
        </button>
        <button
          type="button"
          class="appearance-none bg-red-500 rounded text-white px-3 py-1 text-xs focus:outline-none focus:ring hover:bg-red-600"
          @click="handleDeleteClick"
        >
          deletar
        </button>
      </div>
    </div>
  </template>
  
  <script>
  import { computed } from "vue";
  
  export default {
    props: {
      item: {
        type: Object,
        required: true,
      },
    },
  
    setup(props, { emit }) {
      const formattedTimestamp = computed(() => {
        const date = new Date(props.item.timestamp);
  
        return `${date.toLocaleDateString()} ${date.toLocaleTimeString()}`;
      });
  
      function handleEditClick() {
        emit("edit", props.item);
      }
  
      function handleDeleteClick() {
        emit("delete", props.item);
      }
  
      return {
        formattedTimestamp,
        handleEditClick,
        handleDeleteClick,
      };
    },
  };
  </script>