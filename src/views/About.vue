<template>
  <div id="container" style="width:500px;height:500px"></div>
</template>

<script>
import Map from "@/util/AMap";
export default {
  name: "home",
  data() {
    return {
      map: null
    };
  },
  created() {
    window.title = "地图";
  },
  mounted() {
    this.initAMap();
  },
  methods: {
    async initAMap() {
      const AMap = await Map();
      console.log(new AMap.CitySearch().getLocalCity);
       new AMap.Map("container", {
        resizeEnable: true, //是否监控地图容器尺寸变化
        zoom: 11, //初始化地图层级
        center: [116.397428, 39.90923] //初始化地图中心点
      });
  
      AMap.plugin("AMap.CitySearch", function() {
        var citySearch = new AMap.CitySearch();
        citySearch.getLocalCity(function(status, result) {
          if (status === "complete" && result.info === "OK") {
          console.log(result+"1111")
          }
        });
      });
    }
  }
};
</script>

<style lang="scss" scoped>
</style>