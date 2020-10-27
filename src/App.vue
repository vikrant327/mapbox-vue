<template>
  

  <div id="app">
    <b-button v-if="hidePanel" class="rotate toggle" v-b-toggle.sidebar-1>Toggle Sidebar</b-button>
    
    <b-sidebar id="sidebar-1" title="Search" width="500px" v-on:hidden="isPanelHide" shadow visible>      
      <div class="px-3 py-2">
           <search @getCurrentLocation="updateCurrentLocation" v-bind:title="searchTitle"/>
           
      </div>
    </b-sidebar>
    
    <mymap v-bind:zoomToLocation="currentLocation" > </mymap>
    <forecasttable style="position: fixed;bottom: 0;right: 0;width: 100%;background:#fff;" />
    
    
  </div>
</template>

<script>
import mymap from './components/map.vue';
import search from './components/search.vue';
import forecasttable from './components/forecasttable.vue';
// Webpack example


export default {
  name: 'App',
  components: {
    mymap,
    search,
    forecasttable
  },
  data: () => {
    return {
        hidePanel:true,
        searchTitle:"Type an Address to Get Location Forecast" ,
        currentLocation:null,   
    }
  },
  methods: {
    isPanelHide: () => {
      return this.hidePanel = true;
    },
    updateCurrentLocation(location){
        console.log("passed location is ",location);
        this.currentLocation = location;
    }
  }
}
</script>

<style >
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  padding:10px;
}




.toggle {
  position:absolute;
  left:-50px;
  top:50%;
  transform: translate(0, -50%);
  z-index:1000;
}

.rotate {

    /* Safari */
    -webkit-transform: rotate(-90deg);

    /* Firefox */
    -moz-transform: rotate(-90deg);

    /* IE */
    -ms-transform: rotate(-90deg);

    /* Opera */
    -o-transform: rotate(-90deg);

}
</style>
