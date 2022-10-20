<template>
  <div
    class="
      flex flex-wrap
      items-center
      shadow
      rounded-2xl
      my-5
      py-3
      pt-z
      pr-4
      pb-3
    "
  >
    <label class="accent-pink-500 pl-4 pt-1.5">
      <input @click="setCheckBox(item.id)" type="checkbox" />
      <!--checkbox-->
    </label>

    <div
      class="pr-2 font-normal text-gray-900 rounded-3xl rounded-l-lg ml-2 pt-1"
    >
      <input
        autofocus
        @keyup.enter="editItem(item)"
        v-model="input"
        type="text"
        :placeholder="item.text"
        v-if="editId == item.id"
      />
      <span class="line-through text-gray-400"
        :class="returnChechboxValue(item.id) ? 'classeRiscada' : 'classePadrao'"
        v-if="editId != item.id"
        >{{ item.text }}</span
      >
      <!-- {{item.text}} -->
      <!-- {{ item.text }} -->
    </div>
    <div class="ml-auto space-x-2">
      <button
        v-if="!setBtnOk"
        type="button"
        class="
          appearance-none
          font-bold
          bg-green-600
          rounded
          text-white
          px-3
          py-1
          text-xs
          focus:outline-none
          focus:ring
          hover:bg-green-500
        "
        @click="setItemToEdit(item)"
      >
        Editar
      </button>

      <button
        v-if="setBtnOk"
        type="button"
        class="
          appearance-none
          font-bold
          bg-green-600
          rounded
          text-white
          px-3
          py-1
          text-xs
          focus:outline-none
          focus:ring
          hover:bg-green-500
        "
        @click="editItem(item)"
      >
        Ok
        
      </button>

      <button
        type="button"
        class="
          appearance-none
          font-bold
          bg-red-900
          rounded
          text-white
          px-3
          py-1
          text-xs
          focus:outline-none
          focus:ring
          hover:bg-red-600
        "
        @click="deleteItem(item.id)"
      >
        Excluir

      </button>
    </div>
  </div>
</template>

<script>
export default {
  data: () => ({
    editId: null,
    input: null,
    isEdit: null,
    setBtnOk: null,
    checkboxList: [],
  }),
  methods: {
    deleteItem(id){
      this.$emit('deleteItem', id)
    },
    returnChechboxValue(id) {
      let contains = this.checkboxList.filter((x) => x == id);
      return contains.length > 0;
    },
    setCheckBox(id) {
      let a = this.checkboxList.filter((x) => x == id);
      if (a.length > 0) {
        this.checkboxList = this.checkboxList.filter((x) => x != id);
      } else {
        this.checkboxList.push(id);
      }
    },
    editItem(item) {
      item.text = this.input;
      this.$emit("edit", item);
      this.setBtnOk = false;
      this.editId = null;
    },
    setItemToEdit(item) {
      
      this.input = item.text;
      this.editId = item.id;
      this.setBtnOk = true;
    },
  },
  props: {
    item: {
      type: Object,
      required: true,
    },
  },
};
</script>

<style scoped>
.classePadrao {
  text-decoration: none;
  color: black;
}
</style>