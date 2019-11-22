<template>
    <div class="map map-16by9">
        <div id="map" ref="map" class="map-item"></div>
    </div>
</template>

<script>
    import GoogleMapsApiLoader from "google-maps-api-loader";
    export default {
        props: {
            longitude: {},
            latitude: {},
            apiKey: {
                required: true,
                type: String
            },
            zoom: {
                default: 10
            },

            withMarker:{
                description: 'Show or Hide Marker(s)',
                default: false,
                type: Boolean
            },

            locations:{
                type: Array,
                required: false
            }
        },

        data() {
            return{
                marker: null,
                map: null,
                google: null,
            }
        },

        methods: {

            initMap() {

                this.map = new this.google.maps.Map(this.$refs.map, {
                    zoom: this.zoom,
                    center: this.latLng
                });

                if(this.withMarker){
                    for ( var i = 0; i < this.locations.length; i++ ){
                        this.marker = new this.google.maps.Marker({
                            position: this.latLngMethod(this.locations[i].latitude, this.locations[i].longitude),
                            map: this.map,
                            title: this.locations[i].title,
                            animation: google.maps.Animation.DROP,
                            icon: "http://www.google.com/intl/en_us/mapfiles/ms/micons/blue-dot.png"
                        });
                        this.google.maps.event.addListener(this.marker, 'click', this.initInfoWindow(this.marker, this.locations[i].title))
                    }
                }
            },

            latLngMethod(lat, lng){
                return {lat: parseFloat(lat), lng: parseFloat(lng) }
            },

            initInfoWindow(marker, title){
                var infowindow = new this.google.maps.InfoWindow();

                return function() {
                    infowindow.setContent(title);
                    infowindow.open(this.map, marker);
                }
            }
        },

        computed: {
          latLng (){
              return {lat: parseFloat(this.latitude), lng: parseFloat(this.longitude) }
          }
        },

        async mounted() {
            const googleMapApi = await GoogleMapsApiLoader({
                libraries: ['places'],
                apiKey: this.apiKey
            })
            this.google = googleMapApi
            this.initMap();
        }
    }
</script>

<style lang="scss" scoped>
.map {
  position: relative;
  display: block;
  width: 100%;
  padding: 0;
  overflow: hidden;

  &::before {
    display: block;
    content: "";
  }

  .map-item,
  iframe,
  embed,
  object,
  video {
    position: absolute;
    top: 0;
    bottom: 0;
    left: 0;
    width: 100%;
    height: 100%;
    border: 0;
  }
}

.map-21by9 {
  &::before {
    padding-top: percentage(9 / 21);
  }
}

.map-16by9 {
  &::before {
    padding-top: percentage(9 / 16);
  }
}

.map-4by3 {
  &::before {
    padding-top: percentage(3 / 4);
  }
}

.map-1by1 {
  &::before {
    padding-top: percentage(1 / 1);
  }
}

</style>
