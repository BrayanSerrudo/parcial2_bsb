<script setup lang="ts">
import { ref } from 'vue'
import http from '@/plugins/axios'
import router from '@/router'

const props = defineProps<{
  ENDPOINT_API: string
}>()

const ENDPOINT = props.ENDPOINT_API ?? ''
const titulo = ref('')
const sinopsis = ref('')
const director = ref('')
const temporadas = ref('')
const fechaEstreno = ref('')
const categoria = ref('')

async function crearSerie() {
  await http
    .post(ENDPOINT, {
      titulo: titulo.value,
      sinopsis: sinopsis.value,
      director: director.value,
      temporadas: parseInt(temporadas.value),
      fechaEstreno: fechaEstreno.value ? new Date(fechaEstreno.value) : null,
      categoria: categoria.value
    })
    .then(() => router.push('/series'))
}
function goBack() {
  router.go(-1)
}
</script>

<template>
  <div class="container">
    <nav aria-label="breadcrumb">
      <ol class="breadcrumb">
        <li class="breadcrumb-item">
          <RouterLink to="/">Inicio</RouterLink>
        </li>
        <li class="breadcrumb-item">
          <RouterLink to="/series">Series</RouterLink>
        </li>
        <li class="breadcrumb-item active" aria-current="page">Crear</li>
      </ol>
    </nav>

    <div class="row">
      <h2>Crear Nueva Serie</h2>
    </div>

    <div class="row">
      <form @submit.prevent="crearSerie">
        <div class="form-floating mb-3">
          <input type="text" class="form-control" v-model="titulo" placeholder="Titulo" required />
          <label for="titulo">Titulo</label>
        </div>
        <div class="form-floating mb-3">
          <input type="text" class="form-control" v-model="sinopsis" placeholder="Sinopsis" required />
          <label for="sinopsis">Sinopsis</label>
        </div>
        <div class="form-floating mb-3">
          <input type="text" class="form-control" v-model="director" placeholder="Director" required />
          <label for="director">Director</label>
        </div>
        <div class="form-floating mb-3">
          <input type="text" class="form-control" v-model="temporadas" placeholder="Temporadas" required />
          <label for="temporadas">Temporadas</label>
        </div>
        <div class="form-floating mb-3">
          <input type="date" class="form-control" v-model="fechaEstreno" placeholder="FechaEstreno" required />
          <label for="fechaEstreno">FechaEstreno</label>
        </div>
        <div class="form-floating mb-3">
          <input type="text" class="form-control" v-model="categoria" placeholder="Categoria" required />
          <label for="categoria">Categoria</label>
        </div>
        <div class="text-center mt-3 mb-3">
          <button type="submit" class="btn btn-primary btn-lg">Crear</button>
        </div>
      </form>
    </div>
    <div class="text-left">
      <button class="btn btn-link" @click="goBack">Volver</button>
    </div>
  </div>
</template>

<style></style>
