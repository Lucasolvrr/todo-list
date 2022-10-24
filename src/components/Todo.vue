<template>
  <div class="font-sans font-thin space-y-4">
    <div>
      <h1 class="font-sans font-light text-center pb-2 text-4xl text-slate-800">
        Minhas tarefas
      </h1>
      <p class="text-l text-center font-light mb-8">

        Você tem <strong>{{ items.length }}</strong> {{taskText}}.

      </p>
    </div>
    <div>
  
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

  data:() => ({

    items: [],
    item: [],
    textValue: null,
    itemToEdit: null,

  }),

  computed: {
     taskText(){
      return this.items.length !== 1 ? "tarefas" : "tarefa" 
     }
  },

  methods: {

    deleteItem(item) {

      let allItensFromLocalStorage = JSON.parse(localStorage.getItem("item"));
      let finalList = allItensFromLocalStorage.filter((x) => x.id != item.id);
      localStorage.setItem("item", JSON.stringify(finalList));
      this.getItems();

    },  

    edit(item) {

      let getItems = this.items.findIndex((item) => item.id === item.id);
      this.items.splice(getItems, item);
      localStorage.setItem("item", JSON.stringify(this.items));

    },
    saveItem(v) {

      localStorage.setItem("item", JSON.stringify(this.addNewItem(v)));
      this.getItems();

    },
    getItems() { 
      let a = JSON.parse(localStorage.getItem("item"));
      this.items = a;

    },

    findItemIndex(id) {
      let items = JSON.parse(localStorage.getItem("item"));
      let a = items.findIndex((item) => item.id === id);
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

   created(){
    let a = [];
    localStorage.setItem("item", JSON.stringify(a))
  } 
};

</script>