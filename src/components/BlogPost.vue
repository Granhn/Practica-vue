<script setup>
//const props = defineProps(['titulo','cuerpo'])
defineProps({
    title:String,
    body:{
        type:String,
        default: "Noticia por defecto"
    },
    id:Number,
    cambiarFavorito:Function
})
//console.log(props)
const emit = defineEmits(['cambiarFavoritoNombre'])
</script>

<template>
    <div class="card">
        <div class="card-body">
            <h5 class="card-tittle">{{ title }}</h5>
            <p>{{ body }}</p>
            <span>ID : {{ id }}</span>
            <button
                class="btn btn-outline-primary" 
                @click="emit('cambiarFavoritoNombre',title)">Convertir favorita!
                <!--@click="cambiarFavorito"!-->
            
            </button>
        </div>
    </div>
</template>

<style>
p, h5,span{
    color: purple;
}
</style>