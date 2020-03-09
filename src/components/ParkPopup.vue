<template>
  <mgl-popup>
    <div class="park">
      <p class="caption">Park Id: {{ park.park_id }}</p>
      <h5>{{ park.park_name }}</h5>
      <p class="location">
        <b>Location:</b> {{ park.location_description }}
      </p>
      <p class="district" v-if="park.cca">
        <b>Area:</b> {{ park.cca }}
      </p>
      <p class="district" v-if="park.district">
        <b>District:</b> {{ park.district }}
      </p>
      <p>
        <a :href="`/park/${park.park_id}`">Learn More>></a>
      </p>
    </div>
  </mgl-popup>
</template>

<script>
import { MglPopup } from 'vue-mapbox';

export default {
  name: 'ParkPopup',
  components: { MglPopup },
  props: ['park'],
};
</script>

<style lang="scss">
.park {
  & > * {
    margin: 0;
    font-family: 'Sen', sans-serif;
  }

  h5 {
    font-weight: bold;
  }

  font-size: 16px;

  .caption {
    font-size: 12px;
    opacity: 0.6;
  }

  p {
    b {
      opacity: 0.8;
    }
    margin: 8px 0;

    &:last-of-type {
      margin-top: 20px;
    }
  }
}

.mapboxgl-popup-close-button {
  font-size: 18px ;
}
</style>
