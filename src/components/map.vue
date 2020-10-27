<template>
  <MglMap :accessToken="accessToken" :mapStyle="mapStyle" @load="onMapLoad" :center="center" :zoom="zoom" @click="mapClicked" />
</template>


<script>
import Mapbox from "mapbox-gl";
import { MglMap } from "vue-mapbox";

const mapBoxToken = "";

export default {
    name:"mymap",
    props:{
        zoomToLocation: {
            type:Object
        }
    },
    components: {
        MglMap
    },
    data() {
        return {
            accessToken:,
            mapStyle:"mapbox://styles/mapbox/light-v10",
            center: [-93.59179687498357, 44.66995747013945],
            zoom: 11,
        }
    },
    created() {
        this.map = null;
        this.mapbox = Mapbox;
    },
    methods: {
        onMapLoad(event) {
            console.log(event);
            this.map = event.map;
            //this.$store.map = event.map;
        },
        mapClicked(event){
            console.log(event);
        }
    },
    watch:{
        zoomToLocation : function(val) {
            console.log(val);
            //this.center = [val.lat,val.lon];
            //this.zoom =  12;
            //this.map.zoomTo(5);
            this.map.flyTo({
                // These options control the ending camera position: centered at
                // the target, at zoom level 9, and north up.
                center: [val.lon,val.lat],
                zoom: 14,                
                // this animation is considered essential with respect to prefers-reduced-motion
                essential: true
            });
            
        }
    }
}
</script>

<style scoped>
.mgl-map-wrapper {
      position:absolute;
      width:100%;
      height:100%;
      border:1px solid grey;
  }
</style>