<template>
  <div class="hello">
    <div :id="divId" class="ashish-google-maps">maps</div>
  </div>
</template>

<script lang="ts">
import { Options, Vue } from "vue-class-component";
declare const google: any;
@Options({
  data() {
    return {
      divId: "",
      customMarkers: []
    };
  },
  props: {
    markers: [],
    latLong: {}
  },
  created() {
    this.divId = this.generateDynamicString(8);
    setTimeout(() => {
      this.loadMap();
    }, 0);
  },
  methods: {
    loadMap() {
      const googleInit = this.getGoogleInitData(
        this.latLong.lat,
        this.latLong.long
      );
      this.nMap = new google.maps.Map(
        document.getElementById(this.divId),
        googleInit
      );
      this.renderMarkers(this.latLong);
    },
    getGoogleInitData(lattitude: string, longtitude: string) {
      return {
        zoom: 16,
        center: new google.maps.LatLng(lattitude, longtitude),
        styles: [
          {
            featureType: "administrative.country",
            elementType: "geometry",
            stylers: [{ visibility: "simplified" }, { hue: "#ff0000" }]
          }
        ]
      };
    },
    renderMarkers(event: any) {
    const lat = event.long;
    const lng = event.long;
    const R = this.radius; // radius of earth in km
    
    // window.console.log(this.nMap.marker, '70');
    // return;
    for (let i = 0; i < this.markers.length; i++) {
      const currentLat = this.markers[i].lat;
      const currentLong = this.markers[i].long;
      const currentType = this.markers[i].type;

      const marker = new google.maps.Marker({
        position: new google.maps.LatLng(currentLat, currentLong),
        map: this.nMap,
        label: {
          text: currentType,
          fontWeight: 'normal',
          fontSize: '14px',
          color: 'white'
        }
      });

      marker.setValues({ id: i, type: currentType });
			((marker, l) => {
				google.maps.event.addListener(marker, 'click', () => {
          this.$emit('markerClicked', {rowClicked: l});
				});
			})(marker, i);
			this.customMarkers.push(marker);
    }
  },

    generateDynamicString(length: number) {
      let result = "";
      const characters =
        "ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789";
      const charactersLength = characters.length;
      for (let i = 0; i < length; i++) {
        result += characters.charAt(
          Math.floor(Math.random() * charactersLength)
        );
      }
      return result;
    },
  },
})
export default class GoogleMaps extends Vue {
  msg!: string;
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
.ashish-google-maps {
    position: inherit !important;
}
</style>
