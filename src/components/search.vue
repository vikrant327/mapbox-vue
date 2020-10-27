<template>
    <div>
    <label>{{title}}</label>
    <b-form  @submit="onSubmit" inline>
        <label class="sr-only" for="inline-form-input-name">Search Location</label>
        <b-input
        id="inline-form-input-name"
        class="mb-2 mr-sm-2 mb-sm-0"
        placeholder="Jane Doe"
        v-model="location"
        ></b-input>

        <b-button type="submit" variant="primary">Search</b-button>
    </b-form>
    <label v-if="mapLocation">Lat: {{mapLocation.lat}} , long: {{mapLocation.lon}}</label>
    </div>
</template>

<script>

import axios from 'axios';
import { EventBus } from "./event-bus.js";

export default {
    name:"search",
    props:{
        title:{
            type: String
        }
    },
    data: () => {
        return {
            location: "St Paul, MN",
            forecast:[],
            currentLocation:null,
        }
    },
    methods: {
        onSubmit(evt){
            evt.preventDefault();
            
            if(this.location) {

                axios.get('http://localhost:8080/weather',{params:{"address":this.location}})
                .then(response => {
                    
                    if(response.data.forecast.location) {
                        this.currentLocation = response.data.forecast.location;
                        this.forecast.push(response.data.forecast);
                        this.$emit("getCurrentLocation", this.currentLocation);
                        EventBus.$emit("forecast-list-update", this.forecast);
                    }
                    
                })
                .catch(e => {
                    console.log(e);
                })

            }
        }
    },
    computed: {
        mapLocation : function() {
            if(this.currentLocation){               
               const {lat , lon} = this.currentLocation;
               return {lat,lon}
            }else{
                return null;
            }
        }
    }
}
</script>