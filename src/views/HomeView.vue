<template>
  <div class="home">
    <MapView />
  </div>
</template>

<script>
// @ is an alias to /src
import MapView from "@/components/MapView.vue";

export default {
  name: "HomeView",
  components: {
    MapView,
  },
};
</script>
<style lang="scss" scoped>
.home {
  width: 100%;
  height: 100%;
  
}
</style>
