<template>

  <div>
    <button
      name="button"
      class="btn btn-primary"
      @click="addMarker"
    >
      Add a marker
    </button>
    <hr>
    <l-map
      :zoom.sync="zoom"
      :options="mapOptions"
      :center="center"
      :bounds="bounds"
      :min-zoom="minZoom"
      :max-zoom="maxZoom"
      style="height: 500px; width: 100%"
    >
      <l-control-layers
        :position="layersPosition"
        :collapsed="false"
        :sort-layers="true"
      />
      <l-tile-layer
        v-for="tileProvider in tileProviders"
        :key="tileProvider.name"
        :name="tileProvider.name"
        :visible="tileProvider.visible"
        :url="tileProvider.url"
        :attribution="tileProvider.attribution"
        :token="token"
        layer-type="base"
      />
      <l-control-zoom :position="zoomPosition" />
      <l-control-attribution
        :position="attributionPosition"
        :prefix="attributionPrefix"
      />
      <l-control-scale :imperial="imperial" />
      <l-marker
        v-for="marker in markersList"
        :key="marker.id"
        :visible="marker.visible"
        :draggable="marker.draggable"
        :lat-lng.sync="marker.position"
        :icon="marker.icon"
        @click="alert(marker)"
      >
        <l-popup :content="marker.tooltip" />
        <l-tooltip :content="marker.tooltip" />
      </l-marker>
    </l-map>
  </div>
</template>

<script>
import {
  LMap,
  LTileLayer,
  LMarker,
  LTooltip,
  LPopup,
  LControlZoom,
  LControlAttribution,
  LControlScale,
  LControlLayers,
} from 'vue2-leaflet';

const tileProviders = [
  {
    name: 'OpenStreetMap',
    visible: true,
    attribution:
      '&copy; <a target="_blank" href="http://osm.org/copyright">OpenStreetMap</a> contributors',
    url: 'https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png',
  },
  {
    name: 'OpenTopoMap',
    visible: false,
    url: 'https://{s}.tile.opentopomap.org/{z}/{x}/{y}.png',
    attribution:
      'Map data: &copy; <a href="http://www.openstreetmap.org/copyright">OpenStreetMap</a>, <a href="http://viewfinderpanoramas.org">SRTM</a> | Map style: &copy; <a href="https://opentopomap.org">OpenTopoMap</a> (<a href="https://creativecommons.org/licenses/by-sa/3.0/">CC-BY-SA</a>)',
  },
];

export default {
  name: 'Example',
  components: {
    LMap,
    LTileLayer,
    LMarker,
    LTooltip,
    LPopup,
    LControlZoom,
    LControlAttribution,
    LControlScale,
    LControlLayers,
  },
  props: ['onAddMarker', 'markers'],
  data() {
    return {
      center: [50.449, 30.525],
      opacity: 0.6,
      token: 'your token if using mapbox',
      mapOptions: {
        zoomControl: false,
        attributionControl: false,
        zoomSnap: true,
      },
      zoom: 15,
      minZoom: 1,
      maxZoom: 20,
      zoomPosition: 'topleft',
      attributionPosition: 'bottomright',
      layersPosition: 'topright',
      attributionPrefix: 'Vue2Leaflet',
      imperial: false,
      Positions: ['topleft', 'topright', 'bottomleft', 'bottomright'],
      tileProviders,
      markersList: this.markers,
    };
  },
  methods: {
    addMarker() {
      this.onAddMarker();
    },
  },
};
</script>
