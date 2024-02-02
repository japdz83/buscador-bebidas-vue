<script setup>
import { computed, handleError } from 'vue';
import { RouterLink, useRoute } from 'vue-router'
import { useBebidasStore } from '../stores/bebidas'

const route = useRoute()
const store = useBebidasStore()

const paginaInicio = computed(() => route.name === 'inicio')

const handleSubmit = () => {
    //Todo: Validacion del formulario

    store.obtenerRecetas()

}
    
</script>

<template>
    <header 
        class="bg-slate-800"
        :class="{header : paginaInicio}"
    
    >

        <div class="mx-auto container px-5 py-16">
            <div class="flex justify-between items-center">
                <div class="logo">
                    <RouterLink :to="{ name: 'inicio' }"> 
                        <img class="w-32" src="/img/logo.svg" alt="Logotipo" />
                    </RouterLink>
                </div>
                
                <nav class="flex gap-4 text-white">
                    <RouterLink 
                        :to="{name: 'inicio'}"
                        class=" uppercase font-bold"
                        active-class="text-orange-500"
                    >
                        Inicio
                </RouterLink>

                <RouterLink 
                        :to="{name: 'favoritos'}"
                        class=" uppercase font-bold"
                        active-class="text-orange-500"
                    >
                        Favoritos
                </RouterLink>
                </nav>
                
            </div>
            
            <form 
                v-if="paginaInicio"
                class="md:w-1/2 2xl:w1/3 bg-orange-400 my-32 p-10 rounded-lg shadow space-y-6"
                @submit.prevent="handleSubmit"
            >
                <div class="space-y-4">
                    <label 
                        for="ingrediente"
                        class="block text-white uppercase font-extrabold text-lg"
                    > Nombre o Ingredientes</label>
                    <input 
                        id="ingrediente"
                        type="text" 
                        class="p-3 w-full rounded-lg focus:outline-none"
                        placeholder="Nombre o Ingrediente: Ej. Vodka, Tequila, etc..."
                        v-model="store.busqueda.nombre"
                    />
                    
                </div>
                
                <div class="space-y-4">
                    <label 
                        for="ingrediente"
                        class="block text-white uppercase font-extrabold text-lg"
                    > Catagorías</label>
                    
                    <select 
                        id="ingrediente"
                        class="p-3 w-full rounded-lg focus:outline-none"
                        v-model="store.busqueda.categoria"
                    
                    >
                    <option > --- Seleccione --- </option>
                    <option 
                        v-for="categoria in store.categorias"
                        :key="categoria.strCategory"
                        :value="categoria.strCategory"
                    >
                        {{ categoria.strCategory }}
                    </option>
                </select>
                
            </div>
            
            <input 
                type="submit" 
                value="Buscar Recetas"
                class="bg-orange-800 hover:bg-orange-900 cursor-pointer text-white font-extrabold p-2 rounded uppercase w-full"
            />
            
        </form>
        </div>

    </header>
</template>

<style>
    .header {
        background-image: url('/img/bg.jpg');
        background-size: cover;
        background-position: center;
    }
</style>

