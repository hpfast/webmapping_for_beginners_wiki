### Markers, circles and polygons
Add custom markers, circles and polygons to your map. (for example your home address). At least, choose coordinates which are on your map.

:white_check_mark: Add the following to your map:

``` js
var marker = L.marker([42.349239, -71.041342]).addTo(map);
```
> **JS** *`var` stands for variable. Variables store data so that they can be used later on in the program.
> Here the keyword `var` creates a new variable named `marker`. The value stored is a Leaflet marker which is immediatly added to our map.*

:white_check_mark: Add another 4 markers. (friends, places you lived or visited?). Note: do give the ‘var’ another name every time. Example:

``` js
var brewery = L.marker([42.346868, -71.034396]).addTo(map);
```

:white_check_mark: Provide the markers with a pop-up. For the Harpoon Brewery we add the following pop-up:

``` js
var popup = "Write your pop up text here";
brewery.bindPopup(popup); 
``` 

> **JS** *Did you notice a `;` at the end of every statement? The semicolon tells the computer that the statement has ended.*

:white_check_mark: Now place a circle on the map, use your own coordinates:

``` js
var circle = L.circle([42.359116, -71.049592], 500, {
  color: 'red',
  fillColor: '#f03',
  fillOpacity: 0.5
}).addTo(map);
``` 

:white_check_mark: Connect all previous markers with a polygon. Use all previous coordinates and combine them in the right order.

``` js
var polygon = L.polygon([
  [42.349239, -71.041342],
  [42.346868, -71.034396],
  [42.359116, -71.049592]
]).addTo(map);
```

:white_check_mark: Your script should look like the following. Also check the debugger in the browser if everything is correct: `F12`

``` js
<script>
  //initialize the map
  var map = L.map('map').setView([42.3600825, -71.0588801], 12);
  
  //Create baselayer - tiles
  var backgroundMap = L.tileLayer('http://{s}.basemaps.cartocdn.com/light_all/{z}/{x}/{y}.png', {
    attribution: '<a href="http://openstreetmap.org">OpenStreetMap</a>contributors, <a href="http://creativecommons.org/licenses/by-sa/2.0/">CC-BY-SA</a>',
    maxZoom: 19
  });
  
  backgroundMap.addTo(map);
  
  //Add markers
  var brewery = L.marker([42.346868, -71.034396]).addTo(map);
  brewery.addTo(map);
  
  var aquarium = L.marker([42.359116, -71.049592]);
  aquarium.addTo(map);
  
  var hotel = L.marker([42.351340, -71.040495]);
  hotel.addTo(map);
  
  var harvard = L.marker([42.376979, -71.116617]);
  harvard.addTo(map);
  
  //Add pop-ups
  var popup = "The Harpoon Brewery.";
  brewery.bindPopup(popup);
  
  var popup1 = "Do you sleep in the SeaPort Hotel?";
  hotel.bindPopup(popup1)
  
  var popup2 = "The New England Aquarium.";
  aquarium.bindPopup(popup2);
  
  var popup3 = "The Harvard University.";
  harvard.bindPopup(popup3);
  
  //add a circle
  var circle = L.circle([42.359116, -71.049592], 4500, {
    color: 'red',
    fillColor: '#f03',
    fillOpacity: 0.5
  }).addTo(map);  
  
  //add a polygon   
  var polygon = L.polygon([
    [42.346868, -71.034396],
    [42.351340, -71.040495],
    [42.359116, -71.049592],
    [42.376979, -71.116617]
  ]).addTo(map);
</script>
```

> **JS** *The double slashes `//` mark a Single line comment. Any text between `//` and the end of the line will be ignored by JavaScript (will not be executed). JavaScript comments can be used to explain JavaScript code, and to make it more readable.*


### Vector Data

What we just added are vector data layers.
Difference between raster and vector. 

[vector](img/vector_data.png)
[raster](img/raster_data.png)

### GeoJSON

JSON stands for JavaScript Object Notation. 
GeoJSON is a format for encoding a variety of geographic data structures.
This is how it looks like:

``` JSON
{
  "type": "Feature",
  "geometry": {
   "type": "Point",
   "coordinates": [125.6, 10.1]
  },
  "properties": {
   "name": "Dinagat Islands"
  }
}
```

GeoJSON supports the following geometry types: `Point, LineString, Polygon, MultiPoint, MultiLineString, and MultiPolygon`. Geometric objects with additional properties are Feature objects. Sets of features are contained by FeatureCollection objects.

It uses the World Geodetic System 1984, and units of decimal degrees.

More links and info can be found in [[Tips & Tricks]]


### GeoJSON-tilelayer
geoJson is the standard data type to create web maps with. You can add this data as another map layer.

:white_check_mark: Place the vd.geojson file in `yourDirectory`.

:white_check_mark: Plave vd.png in `yourDirectory`.

:white_check_mark: Copy the following script and have a look at your map.

``` js
//geojson without jQuery with xhr define icon first
var vdIcon = L.icon({
  iconUrl: "vd.png",
  iconSize: [20,20]
});

//create the geojson layer
var geojson = L.geoJson(null,{
  pointToLayer: function(feature,latlng){
    return L.marker(latlng, {icon: vdIcon});
  }
}).addTo(map);

//add your geojson data to the layer
var xhr = new XMLHttpRequest();
xhr.open('GET', encodeURI("vd.geojson"));
xhr.onload = function() {
if (xhr.status === 200) {
    geojson.addData(JSON.parse(xhr.responseText));
  } else {
    alert('Request failed.  Returned status of ' + xhr.status);
  }
};
xhr.send();
```

:arrow_right: Continue to [[Leaflet step 3]]