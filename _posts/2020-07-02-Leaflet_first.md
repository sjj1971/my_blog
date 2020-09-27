---
title: "Leaflet - part1"
date: 2020-07-02 00:00:00
categories: programming
---
# Using Leaflet for create basic map
### including Leaflet CSS style and JS
```html
<!-- Leaflet CSS -->
  <link rel="stylesheet" href="https://unpkg.com/leaflet@1.3.3/dist/leaflet.css"
  integrity="sha512-Rksm5RenBEKSKFjgI3a41vrjkw4EVPlJ3+OiI65vTjIdo9brlAacEuKOiQ5OFh7cOI1bkDwLqdLw3Zg0cRJAAQ=="
  crossorigin=""/>
<!-- Leaflet JS -->
  <script src="https://unpkg.com/leaflet@1.3.3/dist/leaflet.js"
  integrity="sha512-tAGcCfR4Sc5ZP5ZoVz0quoZDYX5aCtEm/eu1KhSLj2c9eFrylXZknQYmxUssFaVJKvvc0dJQixhGjG2yXWiV9Q=="
  crossorigin=""></script>
```
### basic method
```js
var myMap = L.map("id_tag",{center:[lat,lng], zoom:6})
L.tileLayer("https://api.mapbox.com/styles/v1/{id}/tiles/{z}...",{
   attribution:...
   tileSize:512,
   maxZoom:18,
   zoomOffset:-1,
   id:"mapbox/streets-v11",
   accessToken:API_KEY
}).addTo(myMap);
//adding marker
var marker = L.marker([lat, lng],{ draggable:true, title: "Marker"}).addTo(myMap)
marker.bindPopup("Marker Text")
```
```js
L.marker([lat, lng],{ draggable:true, title: "Marker"}).bindPopup("Marker Text").addTo(myMap)
```
### Markers
```js
L.marker([lat, lng]).addTo(myMap);
L.circle([lat, lng],{color:"green", fillcolor:"green", fillOpacity:0.75, radius:500}).addTo(myMap);
L.polygon([[lat1,lng1],[lat2,lng2],[lat3,lng4],,,],{color:"green", fillcolor:"green", fillOpacity:0.75}).addTo(myMap);
var line = [[lat1,lng1],[lat2,lng2],[lat3,lng4],,,]; L.polyline(line,{color:"red"}).addTo(myMap);
L.rectangle([[lat1,lng1],[lat2,lng2]],{color:"green",weight:3, stroke:true}).addTo(myMap);
```
### Layer group
```js 
//markers layer group
var cityMarkers = [];
for (var i=0; i<cities.length; i++){
   cityMarkers.push(L.marker(cities[i].location).bindPopup("text"))
};
var cityLayer = L.layerGroup(cityMarkers);
//tile layer group
var light = L.tilelayer();
var dark = L.tilelayer();
var baseMaps = { Light: light, Dark: dark};
//overlay layers
var overlayMaps = { Cities: cityLayer};
//draw map
var myMap = L.map("map_id_html",{center:[lat,lng],zoom:6,layers:[light, cityLayer]});
L.control.layers(baseMaps, overlayMaps).addTo(myMap);
```



