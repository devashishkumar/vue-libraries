<template>
  <div class="home">
    <!-- <img alt="Vue logo" src="../assets/logo.png" /> -->
    <GoogleMaps
      @markerClicked="clickMarkerMethod($event)"
      :markers="markers"
      :latLong="latLong"
    />
  </div>
</template>

<script lang="ts">
import { Options, Vue } from "vue-class-component";
import HelloWorld from "@/components/HelloWorld.vue"; // @ is an alias to /src
import GoogleMaps from "@/components/GoogleMaps.vue"; // @ is an alias to /src

@Options({
  components: {
    GoogleMaps,
  },
  methods: {
    clickMarkerMethod: function(data: any) {
      console.log('clicked row is ',data);
    }
  },
  data() {
    return {
      latLong: {
        lat: 28.5636,
        long: 77.3726,
      },
      markers: [
        {
          lat: 28.5661,
          long: 77.3698,
          type: "Shiv Mandir Barola",
        },
        {
          lat: 28.5666,
          long: 77.3664,
          type: "Budh Bazaar",
        },
        {
          lat: 28.5636,
          long: 77.3656,
          type: "Prayag Hospital",
        },
        {
          lat: 28.5579,
          long: 77.3726,
          type: "Shri Ram Hospital",
        },
        {
          lat: 28.564,
          long: 77.378,
          type: "Post Office Barola",
        },
      ],
    };
  },
})
export default class Home extends Vue {}
</script>
