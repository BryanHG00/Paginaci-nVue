<script setup>
//"normal"
//defineProps(['title','body']);

// si queremos acceder como objeto (ojo acceder, aun sigue como tipo array)
//const props = defineProps(['title','id','body']);
// para acceder seria props.title


//Para pasar los datos como objeto
defineProps({
    title: String,
    id: Number,
    //de la siguiente forma en caso de que se quiera definir un dato por defecto en caso de no recibir
    body:{
        type: String,
        default: "Sin descripción"
    }
})

const emit = defineEmits(['fav'])
</script>

<template>
    <div class="card mb-2">
        <div class="card-body">
            <div class="card-title" :id="id">{{id}} - {{ title }}</div>
            <p>{{ body }}</p>
            <button @click="emit('fav',title)" class="btn btn-outline-primary">Favorito</button>
        </div>
    </div>
</template>