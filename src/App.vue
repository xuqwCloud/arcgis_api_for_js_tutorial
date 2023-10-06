<script setup>
import { onMounted } from "vue"
import Map from "@arcgis/core/Map.js"
import MapView from "@arcgis/core/views/MapView.js"

// 空间查询 api
import * as query from "@arcgis/core/rest/query.js"

// 缓冲区分析 api
import Graphic from "@arcgis/core/Graphic.js"
import GraphicsLayer from "@arcgis/core/layers/GraphicsLayer.js"
import Point from "@arcgis/core/geometry/Point.js"
import * as webMercatorUtils from "@arcgis/core/geometry/support/webMercatorUtils.js"
import * as geometryService from "@arcgis/core/rest/geometryService.js"
import BufferParameters from "@arcgis/core/rest/support/BufferParameters.js"

// 路径分析 api
import * as route from "@arcgis/core/rest/route.js"
import RouteParameters from "@arcgis/core/rest/support/RouteParameters.js"
import Stop from "@arcgis/core/rest/support/Stop.js"
import Collection from "@arcgis/core/core/Collection.js"

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

  // 空间查询
  // let queryUrl =
  //   "https://sampleserver6.arcgisonline.com/arcgis/rest/services/SampleWorldCities/MapServer/0"

  // query
  //   .executeQueryJSON(queryUrl, {
  //     // autocasts as new Query()
  //     where: "POP > 10000000",
  //   })
  //   .then(
  //     function (results) {
  //       // 查询结果
  //       console.log("success", results)
  //     },
  //     function (error) {
  //       console.log("error", error) // 查询失败
  //     }
  //   )

  // 缓冲区分析
  // const bufferLayer = new GraphicsLayer()
  // map.add(bufferLayer)

  // const point = new Point({
  //   x: 15,
  //   y: 65,
  //   spatialReference: view.spatialReference,
  // })
  // const bufferUrl =
  //   "https://sampleserver6.arcgisonline.com/arcgis/rest/services/Utilities/Geometry/GeometryServer"
  // const webMerPoint = webMercatorUtils.geographicToWebMercator(point)
  // const params = new BufferParameters({
  //   distances: [5],
  //   unit: "kilometers",
  //   geodesic: true,
  //   bufferSpatialReference: view.spatialReference,
  //   outSpatialReference: view.spatialReference,
  //   geometries: [webMerPoint],
  // })

  // geometryService.buffer(bufferUrl, params).then(function (results) {
  //   bufferLayer.add(
  //     new Graphic({
  //       geometry: results[0],
  //       symbol: {
  //         type: "simple-fill",
  //         color: [0, 0, 255, 0.5], // 蓝色半透明填充
  //         outline: {
  //           color: "blue",
  //           width: 2,
  //         },
  //       },
  //     })
  //   )
  // })

  // 路径分析
  // const routeUrl =
  //   "https://route-api.arcgis.com/arcgis/rest/services/World/Route/NAServer/Route_World"

  // const stops = new Collection([
  //   new Stop({
  //     geometry: { x: -117.59275, y: 34.062 },
  //     name: "Ontario Airport",
  //   }),
  //   new Stop({
  //     geometry: { x: -117.1957, y: 34.05609 },
  //     name: "Esri Campus",
  //   }),
  // ])

  // const routeParams = new RouteParameters({
  //   apiKey: "YOUR_API_KEY",
  //   stops,
  // })

  // function solveRoute() {
  //   route.solve(routeUrl, routeParams).then(showRouteInfo)
  // }

  // function showRouteInfo(routeSolveResult) {
  //   console.log("Show all results: ", routeSolveResult)
  //   console.log(
  //     "Show the route information: ",
  //     routeSolveResult.routeResults[0].route
  //   )
  // }

  // solveRoute()
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
