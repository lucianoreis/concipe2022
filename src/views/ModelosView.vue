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
    <li
      v-for="modelo in modelos"
      :key="modelo.code"
    >
    {{ modelo.name }}
    </li>
  </div>
</template>

<style>
</style>
