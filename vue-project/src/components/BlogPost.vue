<script setup>
    // defineProps(["title", "body", "colorText"]) // como array

    // 2. props como objeto
    defineProps({
        title: String,
        id: Number,
        body: {
            type: String,
            default: "sin info",
        },
    });

    const emit = defineEmits(['cambiarFavorito'])
</script>

<template>
    <div class="card">
        <div class="card-body">
            <h5 class="text-capitalize">{{ id+'.' }} {{ title }}</h5>
            <p>{{ body }}</p>
    
            <button class="btn btn-secondary" @click="emit('cambiarFavorito', title)">Add favorito</button>
        </div>
    </div>
</template>

<style scoped>
</style>