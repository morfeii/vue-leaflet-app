<template>
  <div>
    <div class="row">
      <div class="col-12">
        <h1 class="text-center text-info">Vue Leaflet App</h1>
      </div>
    </div>
    <div class="row">
      <div class="col-8 ">
          <MarkersList :markers='markers' @removeMarker='onRemove'/>
      </div>
      <div class="col-4">
        <MapLayout :onAddMarker='onAddMarker' :markers='markers' />
      </div>
    </div>
  </div>
</template>

<script>
import { uuid } from 'vue-uuid';
import MarkersList from './MarkersList.vue';
import MapLayout from './MapLayout.vue';


export default {
  name: 'Map',
  components: { MarkersList, MapLayout },
  data() {
    return {
      markers: [
        {
          id: '1',
          position: { lat: 50.449, lng: 30.525 },
          tooltip: 'Tooltip for Marker 1',
          draggable: true,
          visible: true,
        },
      ],
    };
  },
  methods: {
    onAddMarker() {
      const idx = this.markers.length + 1;
      const newMarker = {
        id: uuid.v4(),
        position: { lat: 50.449, lng: 30.525 },
        tooltip: `Tooltip for Marker ${idx}`,
        draggable: true,
        visible: true,
      };
      this.markers.push(newMarker);
    },
    onRemove({ index }) {
      this.markers.splice(index, 1);
    },
  },
};
</script>

<style lang="scss" scoped>
</style>
