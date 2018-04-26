<template>
  <v-map :zoom=10 :center="initialLocation">
    <v-tilelayer-googlemutant :apikey="apikey" :options="options"></v-tilelayer-googlemutant>
  </v-map>
</template>

<script>
  import L from 'leaflet'
  import * as Vue2Leaflet from 'vue2-leaflet'
  import Vue2LeafletGoogleMutant from './Vue2LeafletGoogleMutant'

  export default {
    components: {
      'v-map': Vue2Leaflet.LMap,
      'v-tilelayer': Vue2Leaflet.LTileLayer,
      'v-tilelayer-googlemutant': Vue2LeafletGoogleMutant
    },
    methods: {
    },
    data () {
      let options = {
        type: 'roadmap'
      }
      let apikey = 'YOUR_API_KEY'
      return {
        apikey,
        options,
        initialLocation: L.latLng(-34.9205, -57.953646)
      }
    }
  }
</script>

<style>
  @import "~leaflet/dist/leaflet.css";
  html, body {
    height: 100%;
    margin: 0;
  }
</style>