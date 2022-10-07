<template  >
 
    <div class="border-stone-900 shadow-slate-400 rounded-lg px-10 py-10 mx-auto my-8 w-auto">
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
