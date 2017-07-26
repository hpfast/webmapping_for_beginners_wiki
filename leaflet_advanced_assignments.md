# Adding a custom marker

### Creating a custom icon

Instead of a simple circleMarker we can define our own markers! 
Leaflet has a `L.icon()` function for this.

:arrow_forward: Download the [big_foot_orange.png]() file and place it in `yourDirectory` next to the index.html file.

:arrow_forward: Replace the previous code for the marker and geojson layer with the following code: 

```js
    var bigfootIcon = L.icon({
          iconUrl: 'big_foot_orange.png',
          iconSize:     [15, 25], // size of the icon
    });

    //create the geojson layer
    var geojson = L.geoJson(null,{
      pointToLayer: function (geoJsonPoint, latlng) {
        return L.marker(latlng, {icon: bigfootIcon});
      }
    }).addTo(map);
```

First we define an icon with `L.icon()`. We have given the object a couple of options. Many options are available, but we just need two for now.The url is the path to the image file, in this case the big_foot_orange.png file.  It is in the same directory as the HTML page.

See the [marker docs](http://leafletjs.com/reference-1.1.0.html#marker) and the [icon docs](http://leafletjs.com/reference-1.1.0.html#icon) for all the possibilities!

Then the Geojson layer gets an L.marker instead of a L.circleMarker and the icon is passed in this.

:arrow_forward: Find yourself another nice marker to pass to your map. It can be a .png file but also .gif files are possible! 

# Marker pop up Interactivity

# Multiple layers!

      var backgroundMap = L.tileLayer('http://{s}.basemaps.cartocdn.com/light_all/{z}/{x}/{y}.png', {
        attribution: '<a href="http://openstreetmap.org">OpenStreetMap</a>contributors, <a href="http://creativecommons.org/licenses/by-sa/2.0/">CC-BY-SA</a>',
        maxZoom: 19
      });
      
      
      var secondLayer = L.tileLayer(' http://tile.stamen.com/toner/{z}/{x}/{y}.png', {
        maxZoom: 19
      });
      
      
      var layers = {
        "basic" : backgroundMap,
        "extra" : secondLayer
      }

      backgroundMap.addTo(map);

      // map.layers = [backgroundMap, secondLayer]

      L.control.layers(layers).addTo(map);



## Using JQuery to load geojson

An alternative way to add your .geojson data to your page is using JQuery.

:arrow_forward: In the head add the jquery library 

```html
<script src="http://code.jquery.com/jquery-2.1.0.min.js"></script>
```

:arrow_forward: Instead of the XMLHttp request we can use Jquery to request the json and immediatly pass the data to our allready created geojson layer!

```js
$.getJSON("./All_BFRO_Reports_points.geojson", function(data) {
  geojson.addData(data);
});

```