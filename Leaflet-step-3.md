In Leaflet step 3 we will add a GeoJSON file containing geo-spatial data to our map.

### GeoJSON

[GeoJSON](http://geojson.org/) is the standard data type to create web maps with. You can add this data as another map layer.
The geodata that we want to add will be a GeoJSON file. JSON stands for JavaScript Object Notation. GeoJSON is a format for encoding a variety of geographic data structures.

This is what it looks like:

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

The GeoJSON format specification can be found [here](http://geojson.org/) and [here](https://tools.ietf.org/html/rfc7946).

### Let's add the Bigfoot Sightings Data to our map!

We prepared a dataset for you that contains the viewing sites of bigfoot! The dataset is downloaded on the 3th of May 2017 from the BFRO database. The [BFRO](https://www.bfro.net/) is the only scientific research organization exploring the bigfoot mystery. Data is collected from 1995 till now. We pre-processed their data and exported it to a geojson file. If you want to know more about the Database history or the classification of the data have a look at the [BRFO documentation](https://www.bfro.net/GDB/classify.asp).


For inspiration: the following map is was also made from this dataset.

![bigfoot](http://thumbnails.visually.netdna-cdn.com/SquatchWatch92YearsofBigfootSightingsintheUSandCanada_523b7482cc497.png)


:arrow_forward: Download the [dataset](https://github.com/NieneB/Webmapping_for_beginners/blob/gh-pages/data/All_BFRO_Reports_points.geojson). 

:arrow_forward: Have a look at the file in your browser. Do you see how it is build up?

:arrow_forward: Right click: `Save Page As...`

:arrow_forward: Place the All_BFRO_Reports_points.geojson file in `yourDirectory`.

This is what it looks like:

```json
{
  "type": "FeatureCollection",
  "crs": { 
    "type": "name", 
    "properties": { 
      "name": "urn:ogc:def:crs:OGC:1.3:CRS84" }
    },
  "features": [
    {
      "type": "Feature",
      "properties": { 
        "name": "June 2000", 
        "styleUrl": "#a", 
        "styleHash": "72e6f3ff", 
        "styleMapHash": { "normal": "#anormal", "highlight": "#ahighlighted" }, 
        "description": "\r\n          Report 637: Campers' encounter just after dark in the Wrangell - St. Elias National Park and PreserveClass A; Cordova-McCarthy CountyClick for details(Location look wrong?)", 
        "timestamp": "2000\/06\/16 12:00:00", 
        "stroke-width": null, 
        "fill": null, 
        "fill-opacity": null, 
        "visibility": null 
      }, 
      "geometry": { 
        "type": "Point", 
        "coordinates": [ -142.9, 61.5, 100.0 ] 
      } 
    },
    { 
      "type": "Feature", 
      "properties": { 
        "name": " 1995", 
        "styleUrl": "#a", 
        "styleHash": "72e6f3ff", 
        "styleMapHash": { "normal": "#anormal", "highlight": "#ahighlighted" }, 
        "description": "\r\n          Report 2917: Family observes large biped from carClass A; Prince of Wales CountyClick for details(Location look wrong?)", 
        "timestamp": "1995\/05\/15 12:00:00", 
        "stroke-width": null, 
        "fill": null, 
        "fill-opacity": null, 
        "visibility": null 
      }, 
      "geometry": { 
        "type": "Point", 
        "coordinates": [ -132.7982, 55.1872, 100.0 ] 
      } 
    },
    { .... }
  ]
};
```

:information_source: The GeoJSON file starts with defining its `type`, `crs` and `features`. The `type` is a FeatureCollection, meaning it can contain multiple geometries of type, point, line and polygons combined. 

:information_source: The `crs` is the geographical system the data is in. Here they use WGS84 or Web Mercator projection.

:information_source: All the geometries are in the `features` array. You see 2 point features in this code snippet. But the whole file contains many many more! 


## Running a local server

When developing a website, a web designer needs to be able to see his webpages the same way the end user would. Sometimes simply clicking on and viewing your HTML files in the web browser is enough, but if you want to test dynamic content, you will need to set up a local web server. Doing this is quite simple and can easily be accomplished on Windows, Mac, and Linux. There are many types of web servers available, but we will be using the Python's SimpleHTTPServer as it is very easy to set up.

If we want to add the Bigfoot data to our own map, we need to run a local server.

```
python -m SimpleHTTPServer [port]
```
If you do not know how to do this then follow the [[Running a local server]] first!

Is the server running? Then we can add the code.

## Adding a GeoJSON layer to Leaflet.

:arrow_forward: Copy the following code between your `<script>` tags and after your previous code.


``` js
// Create a marker first
var geojsonMarkerOptions = {
  radius: 8,
  fillColor: "#ff7800",
  color: "#000",
  weight: 1,
  opacity: 1,
  fillOpacity: 0.8
};

//create a empty geojson layer
var geojson = L.geoJson(null,{
  pointToLayer: function (feature, latlng) {
    return L.circleMarker(latlng, geojsonMarkerOptions);
  }
}).addTo(map);
```

This bit of codes, will add a GeoJSON layer to the leaflet map, on top of our background layer. 
First we define a Marker style for our points that we add later.

``` js
var geojsonMarkerOptions = {
  radius: 8,
  fillColor: "#ff7800",
  color: "#000",
  weight: 1,
  opacity: 1,
  fillOpacity: 0.8
};
```

This creates a object `geojsonMarkerOptions` with the properties that define the marker style. The cirlce will be 8 pixels in radius and orange of color. 

GeoJSON objects are added to the map through a GeoJSON layer. To create it and add it to a map, we use the following code:

``` js
L.geoJSON(geojsonFeature, properties).addTo(map);
```

Alternatively, we could create an empty GeoJSON layer and assign it to a variable so that we can add more features to it later.

``` js
var myLayer = L.geoJSON().addTo(map);
myLayer.addData(geojsonFeature);
```

In our example we create a empty geoJSON layer but do define some properties for it already! 

``` js
//create a empty geojson layer
var geojson = L.geoJson(null,{
  pointToLayer: function (geoJsonPoint, latlng) {
    return L.circleMarker(latlng, geojsonMarkerOptions);
  }
}).addTo(map);
```

The `pointToLayer` is a function defining how GeoJSON points spawn Leaflet layers. It is internally called when data is added, passing the GeoJSON point feature and its LatLng. The default is to spawn a default Marker: 

``` js
function(geoJsonPoint, latlng) {
  return L.marker(latlng);
}
```

Instead of the default, we spawn a L.cirlcleMarker here with our predefined options that are stored in the `geojsonMarkerOptions` object.

Now it is time to add the real data to our GeoJSON object, becuase there is nothing to see yet!


## Get GeoJSON data with XMLHttpRequest 

:arrow_forward: Copy the following code between your `<script>` tags and after your previous code.

```js
// new Http Request
var xhttp = new XMLHttpRequest();

// set the request method and data file
xhttp.open('GET', encodeURI("All_BFRO_Reports_points.geojson"));

//specify what must be done with the geojson data to the layer when request is succesfull
xhttp.onload = function() {
  if (xhttp.readyState === 4) {
      // add the json data to the geojson layer we created before!
      geojson.addData(JSON.parse(xhttp.responseText));
    } else {
      alert('Request failed.  Returned status of ' + xhttp.status);
    }
};

// send the request
xhttp.send();
```

> ### XMLHttpRequest
> XMLHttpRequest (XHR) is an API in the form of an object whose methods transfer data between a web browser and a web server. The object is provided by the browser's JavaScript environment. 
> All modern browsers have a built-in XMLHttpRequest object to request data from a server. The XMLHttpRequest object is a developers dream, because you can:
>
>    Update a web page without reloading the page
>    Request data from a server - after the page has loaded
>    Receive data from a server  - after the page has loaded
>    Send data to a server - in the background


The first line in the example above creates an new XMLHttpRequest object:

```js
var xhttp = new XMLHttpRequest();
```

The second line sets a open method which uses the `GET` method on the url on our own local server. 

```js
xhttp.open('GET', encodeURI("./All_BFRO_Reports_points.geojson"));
```

The third part sets what will be invoked on the onreadystatechange. readyState 4 means the HTTP response content has finished loading, the readyState property of the XMLHttpRequest object should be assigned a value of 4 (DONE). Now we can do something with the response! the responseText, is our geoJSON data set! So the geoJSON text from our file is parsed to our geojson layer which we created before!

```js
xhttp.onload = function() {
  if (xhttp.readyState === 4) { 
    geojson.addData(JSON.parse(xhttp.responseText));
  }
  ...
}; 
```

If the readyState is not done, the `else` statement will alert a warning with the xhttp.readyState it is in. 

```js
else {
  alert('Request failed.  Returned status of ' + xhttp.readyState);
}
```

Eventually we will have to send the request.

```js
xhttp.send();
```

So let's have a look if it worked:

:arrow_forward: Refresh your localhost:8000/index.html page. Do you see your data?


Try to fancy up the styling a bit!


:arrow_right: Put your map online with the [[Hosting on Github]] tutorial!

:arrow_right: Continue to [[Introduction D3]] or do the [[Leaflet Advanced assignments]]

In the [[Leaflet Advanced assignments]] you can add your own custom markers or use a extension like drawing your own lines on the map.

:arrow_right: Continue to [[Introduction D3]]
