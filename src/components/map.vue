<template>
  <div>
    <p>Lattitude: {{latitude}}</p>
    <p>longitude: {{longitude}}</p>
    <div id="mapid"></div>
  </div>
</template>



<script>
import L from "leaflet";
export default {
  name: "Map",
  data() {
    return {
      status: true,
      users: [],
      itemRefs: [], // for saving the unique mapid
      location: null,
      latitude: null,
      longitude: null,
      accessToken:
        "pk.eyJ1IjoidmFsb3RpbiIsImEiOiJja3lhNzZ0OGkwMnA2Mm9uMG54YXplbDR5In0.Sd0ADIklcoKZ-g3lv_Ie0A",
    };
  },
  methods: {
    getLocation() {
      if (navigator.geolocation) {
        navigator.geolocation.getCurrentPosition(this.showPosition);
      } else {
        this.location = "Geolocation is not supported by this browser.";
      }
    },
    showPosition(position) {
      (this.latitude = position.coords.latitude),
        (this.longitude = position.coords.longitude);
    },
    /**
     * instantiate the id to each user to further use
     */
    instantiateId() {
      this.users.map((user, index) => (user.id = index));
    },
    setItemRef(el) {
      if (el) {
        // reference: https://v3.vuejs.org/guide/migration/array-refs.html#migration-strategy
        //console.log(el)
        //console.log(el.id)
        this.itemRefs.push(el.id);
      }
    },
    createMap() {
      var mymap = L.map("mapid").setView([51.505, -0.09], 13);
      L.tileLayer(
        "https://api.mapbox.com/styles/v1/{id}/tiles/{z}/{x}/{y}?access_token={accessToken}",
        {
          attribution:
            'Map data &copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors, Imagery © <a href="https://www.mapbox.com/">Mapbox</a>',
          maxZoom: 18,
          id: "mapbox/streets-v11",
          tileSize: 512,
          zoomOffset: -1,
          accessToken: this.accessToken,
        }
      ).addTo(mymap);
    },
  },
  mounted() {
    this.createMap();
    this.getLocation();
  },
};
</script>


<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
#map {
  height: 60vh;
  width: 100vh;
  border: 5px solid black;
}
</style>
