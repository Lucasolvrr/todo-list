<template >
  <form class="flex flex-wrap" @submit.stop.prevent="handleSubmit">
    <div class="flex-1">
      <input
        ref="inputRef"
        v-model="text"
        type="text"
        class="border-slate-600 shadow-md w-full border rounded-full px-3 py-2 focus:outline-none focus:ring text-gray-500 placeholder-gray-500 placeholder-opacity-100"
        placeholder="Digite uma tarefa..."
      />
    </div>
    <div class="ml-4"> 

      <button
        type="submit"
        class="ease-out duration-300 bg-black hover:-translate-y-0.5 hover:scale-100 hover:bg-neutral-900 py-2 px-4 text-white font-semibold rounded-lg shadow-md hover:bg-neutral-900 focus:outline-none focus:ring-2 focus:ring-neutral-700 focus:ring-opacity-75 rounded-full font-bold w-28 py-2 px-3 text-center text-white focus:outline-none focus:ring shadow-md"
        :class="{ 'opacity-90': isDisabled }"
        :disabled="isDisabled"
      >
        {{ isNewItem ? "Adicionar" : "Salvar" }}
        
      </button>
      
    </div>
  </form>
</template>
  
<script>
  import { computed, ref, watch } from "vue"; //e "computed" 'ref' 'watch'
  
  export default {
    props: {
      item: {
        type: Object,
        required: true,
      },
    },
  
    setup(props, { emit }) { //e "emit"
      const inputRef = ref(null);
      const text = ref(props.item.text);
      const isNewItem = computed(() => props.item.id === null);
      const isDisabled = computed(() => text.value.trim().length === 0);
  
      watch(
        () => props.item,
        () => {
          text.value = props.item.text;
          inputRef.value.focus(); // focar no input logo após a mudança?
        }
      );
        
      function handleSubmit() {
        emit("save", { ...props.item, text: text.value }); //salvar após a mudança
      }
  
      return {
        inputRef,
        text,
        isNewItem,
        isDisabled,
        handleSubmit,
      };
    },
  };
  </script>
  