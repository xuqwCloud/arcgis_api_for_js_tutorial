<script setup>
import { onMounted } from "vue"
import Map from "@arcgis/core/Map.js"
import MapView from "@arcgis/core/views/MapView.js"
import AreaMeasurement2D from "@arcgis/core/widgets/AreaMeasurement2D.js"
import BasemapToggle from "@arcgis/core/widgets/BasemapToggle.js"
import Home from "@arcgis/core/widgets/Home.js"

onMounted(() => {
  const map = new Map({
    basemap: "topo-vector",
  })
  const view = new MapView({
    container: "map",
    map: map,
    // zoom: 12, // 缩放级别
    // center: [104.07, 30.66], // 中心点坐标
    rotation: 0, // 倾斜角
  })

  view.zoom = 8
  view.center = [104.07, 30.66]

  // 5秒后跳转到北京
  // setTimeout(() => {
  //   view.goTo({
  //     center: [116.38, 39.87],
  //   })
  // }, 5000)

  // 地图绑定点击事件
  view.on("click", function (event) {
    console.log("click", event.mapPoint)
  })

  // 添加面积测量工具 2D
  const measurementWidget = new AreaMeasurement2D({
    view: view,
  })
  view.ui.add(measurementWidget, "top-right")

  // 添加底图切换
  const basemapToggle = new BasemapToggle({
    view: view,
    nextBasemap: "osm",
  })
  view.ui.add(basemapToggle, "bottom-right")

  // 添加 Home 按钮
  const homeWidget = new Home({
    view: view,
  })

  view.ui.add(homeWidget, "top-left")
  // 5秒后销毁 Home 按钮
  setTimeout(() => {
    homeWidget.destroy()
  }, 5000)
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
