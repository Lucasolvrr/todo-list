<template>
  <div class="">
    <TodoListItem
      v-for="item in items"
      :key="item.id"
      :item="item"
      @edit="edit(item)"
      @deleteItem="deleteItem(item)"
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
    itemToEdit: null,
    items: {
      type: Array,
      required: true,
    },
  },
  methods: {
    edit(id) {
      this.$emit("edit", id);
    },
    deleteItem(val)
    {
      this.$emit("deleteItem", val);
    }
  },
};
</script>