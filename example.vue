<template>
  <v-map :zoom=10 :center="initialLocation">
    <v-tilelayer-googlemutant :apikey="apikey" :options="options"></v-tilelayer-googlemutant>
  </v-map>
</template>

<script>
  import { latLng } from 'leaflet'
  import { LMap, LTileLayer } from 'vue2-leaflet'
  import Vue2LeafletGoogleMutant from './Vue2LeafletGoogleMutant'

  export default {
    components: {
      'v-map': LMap,
      'v-tilelayer': LTileLayer,
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
        initialLocation: latLng(-34.9205, -57.953646)
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