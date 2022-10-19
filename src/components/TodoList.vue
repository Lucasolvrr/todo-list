<template>
  <div class=""> 
    <TodoListItem
      v-for="item in items"
      :key="item.id"
      :item="item"
      @edit="handleEdit"
      @delete="handleDelete"
      :batata="setValue"
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
    setValue: null
  },

  setup(_, { emit }) {            // e 'emit'
    function handleEdit(item) {
      debugger
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