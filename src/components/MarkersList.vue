<template>
    <div>
      <h3>List of Markers</h3>
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
            v-for="(item, index) in markers1"
            :key="index"
          >
            <td>{{ index + 1 }}</td>
            <td>
              <input
                v-model.number="item.position.lat"
                type="number"
              >
            </td>
            <td>
              <input
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
            <td style="text-align: center">
              <input
                class="form-check-input position-static"
                v-model="item.draggable"
                type="checkbox"
              >
            </td>
            <td style="text-align: center">
              <input
                v-model="item.visible"
                type="checkbox"
              >
            </td>
            <td style="text-align: center">
              <input
                class="btn btn-danger"
                type="button"
                value="X"
                @click="removeMarker(index)"
              >
            </td>
          </tr>
        </tbody>
      </table>
    </div>
</template>

<script>
export default {
  props: ['markers', 'onRemoveMarker'],
  data() {
    return {
      markers1: this.markers,
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

</style>
