<script setup>
    defineProps(["inicio", "fin","postlen"]);
    const emitir = defineEmits(['next','prev']);
</script>
<template>
    <div class="btn-group m-1" role="group" aria-label="Basic example">
        <button class="btn btn-outline-primary" @click="emitir('prev')" :disabled="inicio <= 0">
            Prev {{ inicio }}
        </button> 
        <button class="btn btn-outline-primary" @click="emitir('next')" :disabled="fin >= postlen">
            Next {{ fin }}
        </button>
    </div>
</template>