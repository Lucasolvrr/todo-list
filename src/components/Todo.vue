<template>
  <div class="font-sans font-thin space-y-4">
    <div>
      <h1 class="font-sans font-light text-center pb-2 text-4xl text-slate-800">
        Minhas tarefas
      </h1>
      <p class="text-l text-center font-light mb-8">
        Você tem {{ items.length }} tarefas.
      </p>
    </div>
    <div>
      <v-text-field color="purple"></v-text-field>
      <TodoForm @save="saveItem" />
    </div>
    <div>
      <TodoList
        :items="items"
        @edit="edit"
        @deleteItem="deleteItem"
        :itemToEdit="itemToEdit"
      />
    </div>
  </div>
</template>

<script>
import TodoForm from "./TodoForm.vue";
import TodoList from "./TodoList.vue";
export default {
  components: {
    TodoForm,
    TodoList,
  },
  data: () => ({
    items: [],
    item: [],
    textValue: null,
    itemToEdit: null,
  }),
  methods: {
    deleteItem(item) {
      var allItensFromLocalStorage = JSON.parse(localStorage.getItem("item"));
      var finalList = allItensFromLocalStorage.filter((x) => x.id != item.id);
      localStorage.setItem("item", JSON.stringify(finalList));
      this.getItems();
    },
    edit(item) {
      var batata = this.items.findIndex((item) => item.id === item.id);
      this.items.splice(batata, item);
      localStorage.setItem("item", JSON.stringify(this.items));
    },
    saveItem(v) {
      localStorage.setItem("item", JSON.stringify(this.addNewItem(v)));
      this.getItems();
    },
    getItems() {
      debugger
      var a = JSON.parse(localStorage.getItem("item"));
      this.items = a;
    },
    findItemIndex(id) {
      var items = JSON.parse(localStorage.getItem("item"));
      var a = items.findIndex((item) => item.id === id);
      return a;
    },
    addNewItem(item) {
      this.items.push({
        id: this.items.length,
        text: item,
      });
      return this.items;
    },
  },
  mounted() {
    this.getItems();
  
  },

  // created(){
  //   debugger
  //   var a = [];
  //   a.push({id: 1, text: "teste"})
  //   localStorage.setItem("item", JSON.stringify(a))
  // }

};
</script>