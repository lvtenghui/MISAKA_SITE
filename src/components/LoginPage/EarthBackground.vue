
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
            pitch: 15,
            style: "mapbox://styles/mapbox/satellite-streets-v12",
            language: 'zh-Hans',
        });
        map.on('style.load', () => {
            map.setFog({
                "range": [0.8, 8],
                "color": "#ffefef",
                "horizon-blend": 0.3,
                "high-color": "#245bde",
                "space-color": "#000000",
                "star-intensity": 1
            });
            spinGlobe();
            map.addSource('mapbox-dem', {
                'type': 'raster-dem',
                'url': 'mapbox://mapbox.mapbox-terrain-dem-v1',
                'tileSize': 512,
                // 'maxzoom': 4
            });
            // add the DEM source as a terrain layer with exaggerated height
            map.setTerrain({ 'source': 'mapbox-dem', 'exaggeration': 30 });
            axios({
                methods: 'get',
                url: 'https://efb.xflysim.com/map/data/getOnline.php'
            }).then(function (data) {
                var onlineData = data.data;
                map.addSource('ctrData', {
                    type: 'geojson',
                    data: onlineData.ctr,
                });
                map.addSource('flightData', {
                    type: 'geojson',
                    data: onlineData.flight,
                });
                map.addSource('vaData', {
                    type: 'geojson',
                    data: onlineData.va,
                });
                map.addSource('simData', {
                    type: 'geojson',
                    data: onlineData.sim,
                });
                map.addSource('appData', {
                    type: 'geojson',
                    data: onlineData.app,
                });
                map.addSource('twrData', {
                    type: 'geojson',
                    data: onlineData.twr,
                });
                map.addSource('atisData', {
                    type: 'geojson',
                    data: onlineData.atis,
                });
                map.addSource('fssData', {
                    type: 'geojson',
                    data: onlineData.fss,
                });
                map.loadImage('../../src/assets/map/plane.png', function (error, image) {
                    if (error) throw error;
                    map.addImage('plane', image);
                });
                map.loadImage('../../src/assets/map/vaPlane.png', function (error, image) {
                    if (error) throw error;
                    map.addImage('vaPlane', image);
                });
                map.loadImage('../../src/assets/map/atis.png', function (error, image) {
                    if (error) throw error;
                    map.addImage('atis', image);
                });
                map.loadImage('../../src/assets/map/twr.png', function (error, image) {
                    if (error) throw error;
                    map.addImage('twr', image);
                });

                map.addLayer({
                    'id': 'fssfirboundaries',
                    'type': 'fill',
                    'source': 'fssData',
                    'paint': {
                        'fill-color': '#DC3545',
                        'fill-opacity': [
                            'case',
                            ['boolean', ['feature-state', 'hover'], false],
                            0.6,
                            0.4
                        ]
                    },
                    'maxzoom': 12,
                });

                map.addLayer({
                    'id': 'fssfirboundaries-stroke',
                    'type': 'line',
                    'source': 'fssData',
                    'layout': {},
                    'paint': {
                        'line-color': 'white',
                        'line-opacity': 1,
                        'line-width': 2,
                    },
                    'maxzoom': 12,
                });


                map.addLayer({
                    'id': 'ctrfirboundaries',
                    'type': 'fill',
                    'source': 'ctrData',
                    'paint': {
                        'fill-color': '#FFC107',
                        'fill-opacity': [
                            'case',
                            ['boolean', ['feature-state', 'hover'], false],
                            0.6,
                            0.4
                        ]
                    },
                    'maxzoom': 12,
                });

                map.addLayer({
                    'id': 'ctrfirboundaries-stroke',
                    'type': 'line',
                    'source': 'ctrData',
                    'layout': {},
                    'paint': {
                        'line-color': 'white',
                        'line-opacity': 1,
                        'line-width': 2,
                    },
                    'maxzoom': 12,
                });

                map.addLayer({
                    'id': 'simtraconboundaries',
                    'type': 'fill',
                    'source': 'simData',
                    'paint': {
                        'fill-color': 'yellow',
                        'fill-opacity': [
                            'case',
                            ['boolean', ['feature-state', 'hover'], false],
                            0.6,
                            0.4
                        ]
                    },
                    'maxzoom': 12,
                });

                map.addLayer({
                    'id': 'simtraconboundaries-stroke',
                    'type': 'line',
                    'source': 'simData',
                    'layout': {},
                    'paint': {
                        'line-color': 'white',
                        'line-opacity': 1,
                        'line-width': 2,
                    },
                    'maxzoom': 12,
                });

                map.addLayer({
                    'id': 'apptraconboundaries',
                    'type': 'fill',
                    'source': 'appData',
                    'paint': {
                        'fill-color': '#0DCAF0',
                        'fill-opacity': [
                            'case',
                            ['boolean', ['feature-state', 'hover'], false],
                            0.6,
                            0.4
                        ]
                    },
                    'maxzoom': 12,
                });

                map.addLayer({
                    'id': 'apptraconboundaries-stroke',
                    'type': 'line',
                    'source': 'appData',
                    'layout': {},
                    'paint': {
                        'line-color': 'white',
                        'line-opacity': 1,
                        'line-width': 2,
                    },
                    'maxzoom': 12,
                });

                map.addLayer({
                    'id': 'twr',
                    'type': 'symbol',
                    'source': 'twrData',
                    'layout': {
                        'icon-image': 'twr',
                        'icon-size': 1,
                        "icon-ignore-placement": true,
                    },
                    'minzoom': 0,
                    'maxzoom': 0
                });

                map.addLayer({
                    'id': 'atis',
                    'type': 'symbol',
                    'source': 'atisData',
                    'layout': {
                        'icon-image': 'atis',
                        'icon-size': 1,
                        "icon-ignore-placement": true,
                    },
                    'minzoom': 0,
                    'maxzoom': 0
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


                map.addLayer({
                    'id': 'va',
                    'type': 'symbol',
                    'source': 'vaData',
                    'layout': {
                        'icon-image': 'vaPlane',
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
                var onlineData = data.data;
                map.getSource('flightData').setData(onlineData.flight);
                map.getSource('vaData').setData(onlineData.va);
                map.getSource('atisData').setData(onlineData.atis);
                map.getSource('simData').setData(onlineData.sim);
                map.getSource('twrData').setData(onlineData.twr);
                map.getSource('appData').setData(onlineData.app);
                map.getSource('ctrData').setData(onlineData.ctr);
                map.getSource('fssData').setData(onlineData.fss);
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
    <div id="bulr" style="position: absolute;backdrop-filter: blur(4px);z-index: 2;width: 100vw;height: 100%;"></div>
    <div id="map" style="position: absolute;width: 205vw;height: 100%;z-index: 1; max-width: none; left: -105vw"></div>
</template>