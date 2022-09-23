<script setup>
import { onMounted, ref } from "vue"
const marcas = ref([])
const getBrands = (vehiclesType) => {
  fetch(`https://parallelum.com.br/fipe/api/v2/${vehiclesType}/brands`)
    .then(response => response.json())
    .then(data => {
      marcas.value = data
    })
}
onMounted(() => {
})
const texto = ref("CONCIPE")
</script>
<template>
<div>
  <select>
    <option value="cars" @click="getBrands('cars')">Carros</option>
    <option value="motorcycles" @click="getBrands('motorcycles')">Motos</option>
    <option value="trucks" @click="getBrands('trucks')" >Caminhões</option>
  </select>
</div>
<ul>
  <li v-for="marca in marcas" :key="marca.code">
    {{ marca.name }}
  </li>
</ul>
</template>

<style>
</style>
