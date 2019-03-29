<template>
  <div style="display: none;">
    <slot v-if="ready"></slot>
  </div>
</template>

<script>
import L from 'leaflet'
import 'leaflet.gridlayer.googlemutant'

import { findRealParent, propsBinder } from 'vue2-leaflet'

const props = {
  options: {
    type: Object,
    default() { return {}; },
  },
  apikey: {
    type: String,
    default() { return ''; },
  },
  lang: {
    type: String,
    default: null
  },
  region: {
    type: String,
    default: null
  },
  name: {
    type: String,
    default: ''
  },
  layerType: {
    type: String,
    default: 'base'
  },
  visible: {
    type: Boolean,
    default: true,
  },
};

export default {
  props,
  data() {
    return {
      ready: false,
    };
  },
  mounted() {
    this.mapObject = L.gridLayer.googleMutant(this.options);
    L.DomEvent.on(this.mapObject, this.$listeners);
    propsBinder(this, this.mapObject, props);

    if (!(typeof google === 'object' && typeof google.maps === 'object')) {
      let googleapisscript = document.createElement('script');
      let scriptUrl = 'https://maps.googleapis.com/maps/api/js?key='+this.apikey;
      
      scriptUrl += this.lang ? '&language='+this.lang : '';
      scriptUrl += this.region ? '&region='+this.region : '';
      
      googleapisscript.setAttribute('src', scriptUrl);
      document.head.appendChild(googleapisscript);
    }

    this.ready = true;
    this.parentContainer = findRealParent(this.$parent);
    this.parentContainer.addLayer(this, !this.visible);
  },
  beforeDestroy() {
    this.parentContainer.removeLayer(this);
  },
  methods: {
    addLayer(layer, alreadyAdded) {
      if (!alreadyAdded) {
        this.mapObject.addLayer(layer.mapObject);
      }
    },
    removeLayer(layer, alreadyRemoved) {
      if (!alreadyRemoved) {
        this.mapObject.removeLayer(layer.mapObject);
      }
    },
  },
};
</script>
