<template>
  <div class="MapView">
    <div id="viewDiv">
      <div id="el-select-theme">
        <el-select
          v-model="theme"
          placeholder="请选择"
          @change="BasemapChangeFun"
        >
          <el-option
            v-for="item in options"
            :key="item.value"
            :label="item.label"
            :value="item.value"
          >
          </el-option>
        </el-select>
      </div>
    </div>
  </div>
</template>
<script>
import "@arcgis/core/assets/esri/themes/light/main.css";
import Map from "@arcgis/core/Map";
import MapView from "@arcgis/core/views/MapView";

export default {
  name: "MapView",
  data() {
    return {
      options: [
        {
          value: "dark-gray-vector",
          label: "vector",
        },
        {
          value: "hybrid",
          label: "hybrid",
        },
        {
          value: "topo",
          label: "topo",
        },
        {
          value: "streets",
          label: "streets",
        },
        {
          value: "dark-gray",
          label: "dark-gray",
        },
        {
          value: "osm",
          label: "osm",
        },
        {
          value: "oceans",
          label: "海洋",
        },
      ],
      theme: "",
      mapview: "",
    };
  },
  mounted() {
    this.loadArcgisMap();
  },
  beforeDestroy() {
    this.DestroyArcgisMap();
  },
  methods: {
    loadArcgisMap() {
      const map = new Map({
        basemap: "topo-vector",
      });

      this.mapview = new MapView({
        container: "viewDiv",
        map: map,
        center: [-80, 35],
        extent: {
          spatialReference: {
            latestWkid: 3857,
            wkid: 102100,
          },
          xmin: -59087672,
          ymin: 4108613,
          xmax: -43095009,
          ymax: 8340167,
        },
      });
      this.mapview.ui.components = []; //清空所有ESRI自带的组件

      this.mapview.popup.dockEnabled = false;
      this.mapview.popup.collapseEnabled = false;
      this.mapview.popup.dockOptions = {
        buttonEnabled: false,
        breakpoint: false,
        position: "bottom-left",
      }; //禁用停靠
      this.mapview.popup.actions = null;
      this.mapview.popup = null;
      this.mapview.ui.add("el-select-theme", "top-right");
    },
    BasemapChangeFun(val) {
      this.mapview.map.basemap = val;
    },
    DestroyArcgisMap() {
      this.mapview.destroy();
      this.mapview.map = null;
      this.mapview.container = null;
    },
  },
};
</script>
 
<style  lang="scss" scoped>
.MapView {
  width: 100%;
  height: 100%;
  #viewDiv {
    width: 100%;
    height: 100%;
  }
}
</style>