---
title: "Leaflet - part2"
date: 2020-07-04 12:00:00
categories: programming
---
### Using Geojson
```js
var myMap = L.map("map", {center:[lat,lng],zoom:11});
L.tileLayer().addTo(myMap);
var url = "";
d3.json(link, function(data){
    L.geoJson(data, {
        style:function(feature){
            return{ color:"white", fillcolor: chooseColor(feature.properties.borough), fillOpacity:0.5, weight:1.5}
        },
        onEachFeature: function(feature, layer){
            layer.on({mouseover: function(event){ layer = event.target; layer.setStyle({fillOpacity:0.9})},
                      mouseout: function(event){ layer = event.target; layer.setStyle({fillOpacity:0.5})},
                      click: function(event){myMap.fitBounds(event.target.getBounds())}});
            layer.bindPopup(feature.properties.neighborhood + feature.properties.borough);
        }
    }).addTo(myMap);
});
```
### Add heat layer, marker layer
```js
//marker
var myMap = L.map("map", {center:[lat,lng],zoom:11});
L.tileLayer().addTo(myMap);
d3.json(url, function(response){
   for (i =0; i<response.length, i++){
       var location = response[i].location;
       if(location) {
          L.marker([location.coordinates[1], location.coordinates[0]]).addTo(myMap);
       };
   }
});
//heatmap it used heatmap layer plug-in
var myMap = L.map("map", {center:[lat,lng],zoom:11});
L.tileLayer().addTo(myMap);
d3.json(url, function(response){
   var heatArray=[];
   for (i =0; i<response.length, i++){
       var location = response[i].location;
       if(location) {
          heatArray.push([location.coordinates[1], location.coordinates[0]]);
       };
   };
   var heat = L.heatLayer(heatArray, {radius:20, blur:35}).addTo(myMap);
});
```
```html
<!-- Leaflet heatmap plugin-->
<script type="text/javascript" src="static/js/leaflet-heat.js"></script> 
```
### Marker Cluster
```js
var myMap = L.map("id_html",{center:[lat,lng], zoom:6})
L.tileLayer().addTo(myMap);
d3.json(url, function(response){
    var markers = L.markerClusterGroup();
    for(i=0;i<response.length;i++){
        var location = response[i].location;
        if(location){
            markers.addLayer(L.marker([location.coordinates[1],location.coordinates[0]).bindPoput(response[i].descriptor);
        }
    }
});
```
### Choropleth
```js
var myMap = L.map("map", {center:[lat, lng],zoom:8});
L.tileLayer().addTo(myMap)
var geojson;
d3.json(url,funtion(data){
    geojson = L.chropleth(data, {
        valueProperty: "MHI2016",
        scale: ["#ffffb2","#b10026"],
        steps:10,
        mode:"q",
        style:{color:"#fff",weight:1, fillOpacity:0.8},
        onEachFeature:function(feature,layer){
            layer.bindPopup(feature.properties.Zip + feature.properties.MHI2016);
        };
    }).addTo(myMap);
    var legend = L.control({position: "bottomright"});
    legend.onAdd = function(){
        var div = L.DomUtil.create("div","info legend");
        var limits = geojson.ption.limits;
        var colors = geojson.options.colors;
        var labels = [];
        
        var legendInfo = "";
        div.innerHTML = legendInfo;
        
        limits.forEach(function(liit,index){
            labels.push("*);
        });
        div.innerHTML += "ul" + labels.join("")+"</ul>";
        return div;
    };
    legend.addTo(myMap)    
});
```
