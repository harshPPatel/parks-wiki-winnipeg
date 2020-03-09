<template>
  <div class="wrapper">
    <div class="container" v-if="park">
      <p class="back">
        <a href="/">&lt;&lt; Go Back</a>
      </p>
      <h6>PARK DETAILS</h6>
      <h1>{{ park.park_name }}</h1>
      <h6 class="category">{{ park.park_category.toUpperCase() }}</h6>
      <hr>
      <h6>Details</h6>
      <table>
        <tbody>
          <tr>
            <td>Location</td>
            <td>{{ park.location_description }}</td>
          </tr>
          <tr>
            <td>Neighbourhood</td>
            <td>{{ park.neighbourhood }}</td>
          </tr>
          <tr>
            <td>City Area</td>
            <td>{{ park.cca }}</td>
          </tr>
          <tr>
            <td>District</td>
            <td>{{ park.district }}</td>
          </tr>
          <tr>
            <td>Area <span>(in Hectares)</span></td>
            <td>{{ park.area_in_hectares }}</td>
          </tr>
          <tr>
            <td>
              Water Area <span>(in Hectares)</span>
            </td>
            <td>{{ park.water_area_in_hectares }}</td>
          </tr>
          <tr>
            <td>
              Land Area <span>(in Hectares)</span>
            </td>
            <td>{{ park.land_area_in_hectares }}</td>
          </tr>
          <tr>
            <td>Latitude</td>
            <td>{{ park.location.latitude }}</td>
          </tr>
          <tr>
            <td>Longitude</td>
            <td>{{ park.location.longitude }}</td>
          </tr>
        </tbody>
      </table>
      <div class="about-map">
        <mgl-map
          :accessToken="accessToken"
          mapStyle="mapbox://styles/mapbox/streets-v11"
          :zoom="15"
          :center="mapCenter"
          :interactive="false">
          <mgl-marker :coordinates="mapCenter" color="green" />
        </mgl-map>
      </div>
      <p class="back">
        <a href="/">&lt;&lt; Go Back</a>
      </p>
    </div>
  </div>
</template>

<script>
import {
  MglMap,
  MglMarker,
} from 'vue-mapbox';

import config from '../../config';

export default {
  name: 'Park',
  components: {
    MglMap,
    MglMarker,
  },
  data: () => ({
    park: null,
    accessToken: config.ACCESS_TOKEN,
    mapCenter: null,
  }),
  created() {
    const parkId = this.$route.params.id;
    if (!parkId) {
      this.$router.push({ path: '/404' });
    }
    this.fetchPark(parkId);
    // If park not found, redirect to 404 page
  },
  methods: {
    async fetchPark(id) {
      const API = `https://proxy-server.now.sh/api/v1/winnipeg-parks?park_id=${id}`;
      await fetch(API)
        .then((res) => res.json())
        .then((data) => {
          if (!data.length) {
            this.$router.push({ path: '/404' });
            return;
          }
          // eslint-disable-next-line
          this.park = data[0];
          this.mapCenter = [
            data[0].location.longitude,
            data[0].location.latitude,
          ];
        });
    },
  },
};
</script>

<style lang="scss" scoped>
.wrapper {
  width: 100vw;
  height: 100vh;
  padding-top: 100px;
}

hr {
  margin-bottom: 16px;
}

h6 {
  font-weight: bold;
  opacity: 0.5;
  letter-spacing: 1px;
  margin-bottom: 24px;

  &:last-of-type {
    margin-bottom: 8px;
  }
}

.category {
  margin-top: -16px;
}

.dim {
  opacity: 0.8;
}

tr {
  td:first-of-type {
    font-weight: bold;
    span {
      font-weight: normal;
      font-size: 12px;
    }
  }
}

table {
  min-width: 600px;
  font-size: 16px;
  @media screen and (max-width: 768px) {
    min-width: 80vw;
  }
}

.about-map,
.about-map .mgl-map-wrapper {
  min-height: 300px;
  height: 100%;
  width: 100%;
}

.back {
  margin-top: 32px;
}
</style>
