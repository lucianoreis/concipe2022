<script setup>
import { onMounted, ref } from "vue"
const marcas = ref([])
const getBrands = () => {
  fetch('https://parallelum.com.br/fipe/api/v2/cars/brands')
    .then(response => response.json())
    .then(data => {
      marcas.value = data
    })
}
onMounted(() => {
  getBrands()
})
const texto = ref("CONCIPE")
</script>
<template>
<ul>
  <li v-for="marca in marcas" :key="marca.code">
    {{ marca.name }}
  </li>
</ul>
</template>

<style>
</style>
