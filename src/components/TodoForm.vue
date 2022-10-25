<template>
  <form class="flex flex-wrap">
    <div class="flex-1">
      <input
        ref="inputRef"
        v-model="text"
        type="text"
        name="name" id="name"
        required
        class="
          border-slate-600
          shadow-md
          w-full
          border
          rounded-full
          px-3
          py-2
          focus:outline-none
          focus:ring
          text-gray-500
          placeholder-gray-500 placeholder-opacity-100
        "
        placeholder="Digite uma tarefa..."
      />
    </div>

    <div class="ml-4">  
      <button
        @click.prevent="save"
        type="submit"
        class="
          ease-out
          duration-300
          bg-black
          hover:-translate-y-0.5
          hover:scale-100
          hover:bg-neutral-900
          py-2
          px-4
          text-white
          font-semibold
          rounded-lg
          shadow-md
          hover:bg-neutral-800
          focus:outline-none
          focus:ring-2 focus:ring-neutral-700 focus:ring-opacity-75
          rounded-full
          font-bold
          w-28
          py-2
          px-3
          text-center 
          focus:outline-none
          focus:ring
          shadow-md
        "
        :class="{ 'opacity-90': isDisabled }"
        :disabled="isDisabled"
      >
        Adicionar 

      </button>
    </div>
  </form>

</template>

<script>
export default {
  data: () => ({
    isNewItem: null,
    isDisabled: null,
    text: null,
  }),

  props: { value: null },
  methods: {
    
    save() {
      
      if (!this.text)
      {
           alert("Este campo é obrigatório!")
           return;
      }
      
      this.$emit("save", this.text);
      this.text = "";
    },
  },

  watch: {
    itemToEdit() {
      this.text = this.itemToEdit.text;
    },
  },
};

</script>