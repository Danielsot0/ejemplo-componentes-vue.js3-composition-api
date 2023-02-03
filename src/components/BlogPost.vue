<script setup>

defineProps({
    title: String, 
    id: Number,
    body:{
        type: String,
        default: "sin descripcion",
    },
});

const emit = defineEmits(['CambialFavoritesNombre']);

//emit ('CambialFavorites', title)
</script>

<template>
    <div class="card">
        <div class="card-body">
            <h5 class="card-title">{{ id }} - {{ title }}</h5>
            <p> {{ body }}</p>
            <button @click="emit('CambialFavoritesNombre', title)" class="btn btn-outline-primary">Favorito</button>
        </div>
    </div>
</template>