
<script>
import mapboxgl from "mapbox-gl";
import axios from "axios"
// Vue.prototype.$http = axios
export default {
    name: "mapbox",
    data() {
        return {
            msg: "Welcome to MapBox~",
        };
    },
    mounted() {
        mapboxgl.accessToken = "pk.eyJ1IjoiYmVubWNjbGludG9jayIsImEiOiJjazY1cnBtMTQwMjRkM2tzZnk1MXoyenczIn0.2PyUF_qP-wupcGu-yHaekQ";
        var map = new mapboxgl.Map({
            container: "map",
            center: [113.2, 35.4],
            zoom: 4,
            pitch: 45,
            style: "mapbox://styles/mapbox/satellite-streets-v12",
            language: 'zh-Hans',
        });
        map.on('style.load', () => {
            map.setFog({});
            spinGlobe();
            map.addSource('mapbox-dem', {
                'type': 'raster-dem',
                'url': 'mapbox://mapbox.mapbox-terrain-dem-v1',
                'tileSize': 512,
                // 'maxzoom': 4
            });
            // add the DEM source as a terrain layer with exaggerated height
            map.setTerrain({ 'source': 'mapbox-dem', 'exaggeration': 30 });
            map.loadImage('../../src/assets/plane.png', function (error, image) {
                if (error) throw error;
                map.addImage('plane', image);
            });
            axios({
                methods: 'get',
                url: 'https://efb.xflysim.com/map/data/getOnline.php'
            }).then(function (data) {
                var flightData = data.data.flight;
                map.addSource('flightData', {
                    type: 'geojson',
                    data: flightData,
                });
                map.addLayer({
                    'id': 'flight',
                    'type': 'symbol',
                    'source': 'flightData',
                    'layout': {
                        'icon-image': 'plane',
                        'icon-size': 0.6,
                        'icon-rotate': ['get', 'heading'],
                        'icon-rotation-alignment': 'map',
                        "icon-ignore-placement": true,
                    },
                    'minzoom': 0,
                    'maxzoom': 0,
                });
            })
            setInterval(getOnlineData, 5000);
        });
        function getOnlineData() {
            axios({
                methods: 'get',
                url: 'https://efb.xflysim.com/map/data/getOnline.php'
            }).then(function (data) {
                var flightData = data.data.flight;
                map.getSource('flightData').setData(flightData);
            })
        }
        const secondsPerRevolution = 120;
        const maxSpinZoom = 5;
        const slowSpinZoom = 3;

        let userInteracting = false;

        function spinGlobe() {
            const zoom = map.getZoom();
            if (!userInteracting && zoom < maxSpinZoom) {
                let distancePerSecond = 360 / secondsPerRevolution;
                if (zoom >
                    slowSpinZoom) {
                    const zoomDif =
                        (maxSpinZoom - zoom) / (maxSpinZoom - slowSpinZoom);
                    distancePerSecond *= zoomDif;
                }
                const center = map.getCenter();
                center.lng -= distancePerSecond;
                map.easeTo({
                    center,
                    duration: 1000,
                    easing: (n) => n
                });
            }
        }
        map.on('mousedown', () => {
            userInteracting = true;
        });
        map.on('mouseup', () => {
            userInteracting = false;
            spinGlobe();
        });
        map.on('dragend', () => {
            userInteracting = false;
            spinGlobe();
        });
        map.on('pitchend', () => {
            userInteracting = false;
            spinGlobe();
        });
        map.on('rotateend', () => {
            userInteracting = false;
            spinGlobe();
        });
        map.on('moveend', () => {
            spinGlobe();
        });

    },
};
</script>

<template>
    <!-- <div id="bulr" style="position: absolute;backdrop-filter: blur(4px);z-index: 2;width: 100vw;height: 100%;"></div> -->
    <div id="map" style="position: absolute;width: 100vw;height: 100%;z-index: 1;"></div>
</template>