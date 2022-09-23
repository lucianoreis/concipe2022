<script setup>
import { computed, onMounted, ref } from "vue"
import { useRoute } from 'vue-router'
const route = useRoute()
const modelos = ref([])
const getModels = (vehiclesType, brandId) => {
  fetch(`https://parallelum.com.br/fipe/api/v2/${vehiclesType}/brands/${brandId}/models`)
    .then(response => response.json())
    .then(data => {
      modelos.value = data
    })
}
onMounted(() => {
  getModels(route.params.vehiclesType, route.params.brandId)
})
</script>

<template>
  <div>
    <h1> {{ modelos }}</h1>
  </div>
</template>

<style>
</style>
