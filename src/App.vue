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

  // 地图点击事件
  const clickObj = view.on("click", function (event) {
    // 在此处处理单击事件
    console.log("点击坐标：", event.mapPoint)
  })

  // 地图双击事件
  view.on("double-click", function (event) {
    // 在此处处理双击事件
    console.log("双击坐标：", event.mapPoint)
  })

  // 10s 之后卸载地图点击事件
  setTimeout(() => {
    clickObj.remove()
  }, 10000)
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
