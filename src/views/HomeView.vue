<script setup>
import { computed, onMounted, ref } from "vue"
const marcas = ref([])
const busca = ref('')
const tipo = ref('')
const getBrands = (vehiclesType) => {
  tipo.value = vehiclesType
  fetch(`https://parallelum.com.br/fipe/api/v2/${vehiclesType}/brands`)
    .then(response => response.json())
    .then(data => {
      marcas.value = data
    })
}
const filteredBrands = computed(() => {
  return marcas.value.filter(e => {
    return e.name.toLowerCase().indexOf(busca.value.toLowerCase()) > -1
  })
})
onMounted(() => {
})
const texto = ref("CONCIPE")
</script>
<template>
<div>
  <select>
    <option value="" ></option>
    <option value="cars" @click="getBrands('cars')">Carros</option>
    <option value="motorcycles" @click="getBrands('motorcycles')">Motos</option>
    <option value="trucks" @click="getBrands('trucks')" >Caminhões</option>
  </select>
  <input type="text" v-model="busca" />
</div>
<ul>
  <li
    v-for="marca in filteredBrands"
    :key="marca.code"
    @click="$router.push(`/modelos/${tipo}/${marca.code}`)"
  >
    {{ marca.name }}
  </li>
</ul>
</template>

<style>
</style>
