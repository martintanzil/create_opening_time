<template>
  <div>
    <map-coordinates :lat="mapCoordinates.lat" :lng="mapCoordinates.lng"></map-coordinates>
    <GmapMap 
      :center="startLocation"
      :zoom="15"
      map-type-id="terrain"
      style="width:640px; height:360px"
      ref="mapRef">
      <GmapMarker :position="mapCoordinates"/>
    </GmapMap>
  </div>
</template>

<script>
import MapCoordinates from './components/MapCoordinates.vue'

export default{
  name: 'App',
  components: {MapCoordinates},
  data(){
    return{
      map: null,
      startLocation: {
        lat: 0,
        lng: 0
      }
    }
  },
  created(){
    this.$getLocation({})
    .then(coordinates => {
      this.startLocation = coordinates
      console.log(this.startLocation);
    })
    .catch(error => {
      console.log(error);
    })
  },
  mounted(){
    this.$refs.mapRef.$mapPromise.then(map => this.map = map)
  },
  computed: {
    mapCoordinates(){
      if(!this.map) return this.startLocation
      return { lat: this.map.getCenter().lat(), lng: this.map.getCenter().lng()}
    }
  }
}
</script>

<style>
</style>
