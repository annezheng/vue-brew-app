<template>
  <div class="row map">
    <l-map :zoom="zoom" :center="center" @update:zoom="zoomUpdate" @update:center="centerUpdate">
      <l-tile-layer :url="url" :attribution="attribution"></l-tile-layer>
      <l-marker
        v-for="(brew, index) in brews"
        :key="index"
        :lat-lng="latLng(brew.latitude, brew.longitude)"
        >
        <l-icon :icon-url="icon" :icon-size="brew.iconSize" ></l-icon>
        </l-marker>
    </l-map>
  </div>
</template>

<script>
import {LMap, LTileLayer, LMarker, LIcon } from 'vue2-leaflet';
import logo from '../assets/logo.png'
export default {
  name: 'BrewMap',
  props: {
    brews: Array
  },
  components: {
    LMap,
    LTileLayer,
    LMarker,
    LIcon
  },
  data() {
    return {
      zoom:6,
      center: L.latLng(33.831164, -112.807617),
      currentZoom:6,
      currentCenter: L.latLng(33.831164, -112.807617),
      url:'http://{s}.tile.osm.org/{z}/{x}/{y}.png',
      attribution:'&copy; <a href="http://osm.org/copyright">OpenStreetMap</a> contributors',
      marker: L.latLng(33.831164, -112.807617),
      icon: logo
    }
  },
  methods: {
    latLng (lat, lng) {
      return L.latLng(lat, lng)
    },
    centerUpdate (center) {
      this.currentCenter = center
    },
    zoomUpdate (zoom) {
      this.currentZoom = zoom
    }
  }
}
</script>

<style scoped lang="scss">
.map {
  border: 1px dashed grey;
  height: 90vh;
}
</style>