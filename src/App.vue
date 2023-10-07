<script setup>
import { onMounted } from "vue"
import Map from "@arcgis/core/Map.js"
import SceneView from "@arcgis/core/views/SceneView.js"

onMounted(() => {
  const map = new Map({
    basemap: "topo-vector",
  })
  const view = new SceneView({
    container: "map",
    map: map,
    // center: [-112, 38],
    // zoom: 5,
    camera: {
      position: {
        x: -112, // lon
        y: 38, // lat
        z: 10654, // elevation in meters
      },
      tilt: 45,
    },
  })

  view.ui.components = []
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
