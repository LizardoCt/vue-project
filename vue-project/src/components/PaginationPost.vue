<script setup>
    // defineEmits(['next','prev']) // opcion 1 | con signo ="$emit('next')"
    const emit = defineEmits(['prev', 'next']) // opcion 2

    const activarSgt = () => { // opcion 3 | y se llama a la funcion en el @click='activarSgt'
      emit('next')
    }

    defineProps(["inicio", "fin", "maxLength"]);
</script>

<template>
    <div class="btn-group pb-4">
        <button 
            class="btn btn-secondary"
            @click="emit('prev')"
            :disabled="inicio <= 0"
        >
        Anterior</button>
        
        <button 
          class="btn btn-secondary"
          @click="activarSgt"
          :disabled="fin >= maxLength"
        >
        Siguiente</button>
    </div>
</template>