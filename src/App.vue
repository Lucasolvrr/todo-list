<template >
  <div class="shadow-2xl rounded-lg px-10 py-10  max-w-2xl mx-auto my-8 ">
    <Todo />
  </div>
</template>

<script>
import Todo from "./components/Todo.vue";
export default {
  name: "App",
  components: {
    Todo,
  },
};
</script>

<style>
</style>
