<template>
    <div>
      <h3 class="heading">List of Markers</h3>
      <div class="table-responsive" v-if="markersList.length">
        <table class="table table-striped">
        <thead>
          <tr>
            <th scope="col">Marker</th>
            <th scope="col">Latitude</th>
            <th scope="col">Longitude</th>
            <th scope="col">Tooltip</th>
            <th scope="col">Draggable</th>
            <th scope="col">Visible</th>
            <th scope="col">Remove</th>
          </tr>
        </thead>
        <tbody>
          <tr
            v-for="(item, index) in markersList"
            :key="index"
          >
            <td class="table-data">
              {{ index + 1 }}
            </td>
            <td>
              <input
                class="input-position"
                v-model.number="item.position.lat"
                type="number"
              >
            </td>
            <td>
              <input
                class="input-position"
                v-model.number="item.position.lng"
                type="number"
              >
            </td>
            <td>
              <input
                v-model="item.tooltip"
                type="text"
              >
            </td>
            <td class="table-data">
              <input
                class="form-check-input position-static"
                v-model="item.draggable"
                type="checkbox"
              >
            </td>
            <td class="table-data">
              <input
                class="form-check-input position-static"
                v-model="item.visible"
                type="checkbox"
              >
            </td>
            <td class="table-data">
              <button
                class="btn btn-danger"
                type="button"
                value="X"
                @click="removeMarker(index)"
              >
                <i class="fa fa-trash"/>
              </button>
            </td>
          </tr>
        </tbody>
        </table>
      </div>
      <div class="alert alert-danger" v-else>
        You have no markers!
      </div>
    </div>
</template>

<script>
export default {
  props: ['markers'],
  data() {
    return {
      markersList: this.markers,
    };
  },
  methods: {
    removeMarker() {
      this.$emit('removeMarker', { index: this.index });
    },
  },

};
</script>
<style lang="scss" scoped>
.heading {
  margin-bottom: 20px
}
.table-data {
  text-align: center
}
.input-position {
  width: 100px
}
</style>
