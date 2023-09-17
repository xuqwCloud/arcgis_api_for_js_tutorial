<script setup>
import { onMounted } from "vue"
import Map from "@arcgis/core/Map.js"
import MapView from "@arcgis/core/views/MapView.js"
import FeatureLayer from "@arcgis/core/layers/FeatureLayer.js"
import MapImageLayer from "@arcgis/core/layers/MapImageLayer.js"
import ImageryLayer from "@arcgis/core/layers/ImageryLayer.js"

onMounted(() => {
  const map = new Map({
    basemap: "topo-vector",
  })
  const view = new MapView({
    container: "map",
    map: map,
    zoom: 8,
    center: [-82.44073, 35.613152],
  })

  // 添加要素图层
  const layer1 = new FeatureLayer({
    url: "https://services.arcgis.com/V6ZHFr6zdgNZuVG0/arcgis/rest/services/Landscape_Trees/FeatureServer/0",
  })

  // 改变要素图层的渲染方式-仅改变颜色及外边框
  // layer1.renderer = {
  // type: "simple",  // autocasts as new SimpleRenderer()
  // symbol: {
  //   type: "simple-marker",  // autocasts as new SimpleMarkerSymbol()
  //   size: 6,
  //   color: "black",
  //   outline: {  // autocasts as new SimpleLineSymbol()
  //     width: 0.5,
  //     color: "white"
  //   }
  // }

  // 改变要素图层的渲染方式-改为图片渲染
  // layer1.renderer = {
  //   type: "simple", // autocasts as new SimpleRenderer()
  //   symbol: {
  //     type: "picture-marker", // autocasts as new PictureMarkerSymbol()
  //     url: "https://static.arcgis.com/images/Symbols/Shapes/BlackStarLargeB.png",
  //     width: "32px",
  //     height: "32px",
  //   },
  //   // todo: 报错待调试
  //   // symbol: new PictureMarkerSymbol({
  //   //   type: "picture-marker", // autocasts as new PictureMarkerSymbol()
  //   //   url: "https://static.arcgis.com/images/Symbols/Shapes/BlackStarLargeB.png",
  //   //   width: "32px",
  //   //   height: "32px",
  //   // }),
  // }

  // 改变要素图层的渲染方式-热力图渲染
  // layer1.renderer = {
  //   type: "heatmap",
  //   colorStops: [
  //     { ratio: 0, color: "rgba(255, 255, 255, 0)" },
  //     { ratio: 0.2, color: "rgba(255, 255, 255, 1)" },
  //     { ratio: 0.5, color: "rgba(255, 140, 0, 1)" },
  //     { ratio: 0.8, color: "rgba(255, 140, 0, 1)" },
  //     { ratio: 1, color: "rgba(255, 0, 0, 1)" },
  //   ],
  //   maxPixelIntensity: 100,
  //   minPixelIntensity: 0,
  // }

  // 图层过滤
  //layer1.definitionExpression = "Ht_DBH_ft >= 4.5"

  // 属性查询
  const query = layer1.createQuery()
  query.where = "Ht_DBH_ft >= 5.0"
  layer1.queryFeatures(query).then((result) => {
    // 处理查询结果
    console.log(result.features)
  })
  map.add(layer1)

  // 添加动态图层
  // const layer2 = new MapImageLayer({
  //   url: "https://sampleserver6.arcgisonline.com/arcgis/rest/services/Census/MapServer",
  // })
  // map.add(layer2)

  // 添加影像图层
  // const layer3 = new ImageryLayer({
  //   url: "https://landsat2.arcgis.com/arcgis/rest/services/Landsat8_Views/ImageServer",
  // })
  // map.add(layer3)
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
