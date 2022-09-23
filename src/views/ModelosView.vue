<script setup>
import { computed, onMounted, ref, watch } from "vue"
const modelos = ref([])
const getModels = (vehiclesType, brandId) => {
  fetch(`https://parallelum.com.br/fipe/api/v2/${vehiclesType}/brands/${brandId}`)
    .then(response => response.json())
    .then(data => {
      modelos.value = data
    })
}
onMounted(() => {
})
</script>

<template>
  <div>
    <h1> {{ modelos }}</h1>
  </div>
</template>

<style>
</style>
