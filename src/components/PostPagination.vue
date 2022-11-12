<script setup>

    defineProps(['inicio', 'fin'])

    defineEmits('nextPage', 'prevPage')

</script>

<template>
    <div class="btn-group" role="group" aria-label="Basic example">
        <button 
            :disabled="inicio === 0" 
            type="button" 
            class="btn btn-outline-primary" 
            @click="$emit('prevPage')"
        > Previous {{ inicio }}</button>
        <button
            class="btn btn-outline-primary"
            @click="$emit('nextPage')"
            :disabled="fin === 100" 
            type="button" 
        > Next {{ fin }}</button>
    </div>
</template>