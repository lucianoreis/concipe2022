<script setup>
import { computed, onMounted, ref } from "vue"
import { useRoute } from 'vue-router'
const route = useRoute()
const modelos = ref([])
const busca = ref('')
const filteredModels = computed(() => {
  return modelos.value.filter(e => {
    return e.name.toLowerCase().indexOf(busca.value.toLowerCase()) > -1
  })
})
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
    <input
      type="text"
      v-model="busca"
      placeholder="Busque um modelo"
    />
    <li
      v-for="modelo in filteredModels"
      :key="modelo.code"
    >
    {{ modelo.name }}
    </li>
  </div>
</template>

<style>
</style>
