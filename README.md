# Vue-maps

Vue maps is vue component for usage simple Usage of Google Maps.

[Demo](https://kymrj.csb.app/)
---

# Installation
```
    npm install vue-maps
```

# Import
```
import { GoogleMap } from 'vue-maps'

new Vue({
  components: {
    GoogleMap
  },

  data(){
      return{
        latitude: -33.950198,
        longitude: 151.259302,
        apiKey: "Google Api Key",
        locations: [
            {
                title: "Bondi Beach",
                latitude: -33.890542,
                longitude: 151.274856
            },
            {
                title: "Coogee Beach",
                latitude: -33.923036,
                longitude: 151.259052
            },
            {
                title: "Cronulla Beach",
                latitude: -34.028249,
                longitude: 151.157507
            },
            {
                title: "Manly Beach",
                latitude: -33.80010128657071,
                longitude: 151.28747820854187
            },
            {
                title: "Maroubra Beach",
                latitude: -33.950198,
                longitude: 151.259302
            }
        ]
    }
  }
})
```

# Usage
For Google Maps Usage
```
   <GoogleMap
        :latitude="latitude"
        :longitude="longitude"
        :apiKey="apiKey"
        :zoom="8"
        with-marker
        :locations="locations"
      />
```
# Available Props
| Props | Type | Description |
| ----------- | ----------- |----------- |
| latitude | Float/Integer | Latitude is a measurement on a globe or map of location north or south of the Equator.|
| longitude | Float/Integer | Latitude is a measurement on a globe or map of location east or west of the Equator.|
| zoom | Integer | The maximum zoom level found at the given LatLng. `Default: 10`|
| apiKey | String | Generated on google developers website.|
| with-marker | Boolean | Willing to show marker(s) on Google map. `Default:true`|
| locations | Array | Latitude, Longitude and title of the address(es) you want to show on the map as marker|


### Dependency
This package is dependent on [Google Maps](https://maps.google.com) and [laravel-mix](https://laravel-mix.com/)