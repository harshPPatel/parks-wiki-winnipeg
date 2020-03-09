<template>
  <div class="home">
    <mgl-map
      :accessToken="accessToken"
      :mapStyle="mapStyle"
      :zoom="zoom"
      :center="center"
      :minZoom="13"
      @load="onMapLoaded"
      @moveend="onMapMoveEnded">
      <mgl-fullscreen-control position="bottom-right" />
      <mgl-geolocate-control position="bottom-right" />
      <mgl-marker
        v-for="park in parks"
        :key="park.park_id"
        :coordinates="[park.location.longitude, park.location.latitude]"
        color="green">
        <park-popup :park="park" />
      </mgl-marker>
    </mgl-map>
  </div>
</template>

<script>
import Mapbox from 'mapbox-gl';
import {
  MglMap,
  MglFullscreenControl,
  MglGeolocateControl,
  MglMarker,
} from 'vue-mapbox';

import config from '../../config';

import ParkPopup from '../components/ParkPopup.vue';

export default {
  name: 'Home',
  components: {
    MglMap,
    MglFullscreenControl,
    MglGeolocateControl,
    MglMarker,
    ParkPopup,
  },
  data: () => ({
    accessToken: config.ACCESS_TOKEN,
    mapStyle: 'mapbox://styles/mapbox/streets-v11',
    center: ['-97.138451', '49.895077'],
    currentCordinates: {
      lng: '',
      lat: '',
    },
    zoom: 13,
    parks: [],
  }),
  created() {
    this.mapbox = Mapbox;
  },
  methods: {
    async fetchParks(lng, lat) {
      const API = `http://localhost:5000/api/v1/winnipeg-parks?$where=within_circle(location,${lat},${lng},2000)`;
      await fetch(API)
        .then((res) => res.json())
        .then((data) => {
          this.parks = data;
        });
    },
    onMapLoaded() {
      this.fetchParks(this.center[0], this.center[1]);
    },
    onMapMoveEnded(e) {
      /* eslint-disable no-underscore-dangle */
      const { lng } = e.mapboxEvent.target.transform._center;
      const { lat } = e.mapboxEvent.target.transform._center;
      // Fetching parks
      this.fetchParks(lng, lat);
    },
  },
};
</script>

<style lang="scss">
.home {
  width: 100%;
  min-height: 100vh;
  position: relative;

  .mgl-map-wrapper {
    min-height: 100vh;
  }
}

.loading {
  position: absolute;
  width: 100%;
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
}
</style>
