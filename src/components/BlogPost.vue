<script setup>

    // defineProps(['title', 'id', 'body', 'colorText'])
    defineProps({
        title: String,
        id: Number,
        body: {
            type: String,
            default: 'Sin Descripción'
        }
    })

    const emit = defineEmits(['cambiarFavorito'])

</script>

<template>
    <div class="card">
        <div class="card-body">
            <h5 class="card-title">{{ title }}</h5>
            <p>{{ body }}</p>
            <button @click="emit('cambiarFavorito', title)" class="btn btn-outline-primary"> Favorito </button>
        </div>
    </div>
</template>