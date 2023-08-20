<script setup>
import { onMounted } from "vue"
import Map from "@arcgis/core/Map.js"
import MapView from "@arcgis/core/views/MapView.js"

onMounted(() => {
  const map = new Map({
    basemap: "topo-vector",
  })
  const view = new MapView({
    container: "map",
    map: map,
    zoom: 4,
    center: [15, 65],
  })
})
</script>

<template>
  <div id="map"></div>
</template>

<style scoped>
#map {
  width: 100%;
  height: 100%;
  margin: 0;
}
</style>
