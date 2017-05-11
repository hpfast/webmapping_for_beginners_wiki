### Running a local server

When developing a website, a web designer needs to be able to see his webpages the same way the end user would. Sometimes simply clicking on and viewing your HTML files in the web browser is enough, but if you want to test dynamic content, you will need to set up a local web server. Doing this is quite simple and can easily be accomplished on Windows, Mac, and Linux. There are many types of web servers available, but we will be using the Python's SimpleHTTPServer as it is very easy to set up.


### Of Github.. 


http://www.pythonforbeginners.com/modules-in-python/how-to-use-simplehttpserver/
https://www.maketecheasier.com/setup-local-web-server-all-platforms/



Easy ways of doing this include running Python's SimpleHTTPServer in your map directory, installing MAMP (for Mac), or installing WampServer (for Windows). 



To start a HTTP server on port 8000 (which is the default port), simple type:

```
python -m SimpleHTTPServer [port]
```

This will now show the files and directories which are in the current working
directory.



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


### Vector Data

What we just added are vector data layers.
Difference between raster and vector. 

[vector](img/vector_data.png)
[raster](img/raster_data.png)


http://thumbnails.visually.netdna-cdn.com/SquatchWatch92YearsofBigfootSightingsintheUSandCanada_523b7482cc497.png
### GeoJSON-tilelayer
GeoJSON is the standard data type to create web maps with. You can add this data as another map layer.

:white_check_mark: Download the dataset from https://github.com/NieneB/Webmapping_for_beginners/tree/gh-pages/data

:white_check_mark: Place the BFRO_bigfootA.geojson or BFRO_bigfootb.geojson file in `yourDirectory`.

:white_check_mark: Copy the following script and have a look at your map.

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

//create the geojson layer
var geojson = L.geoJson(geojsonFeature,{
  pointToLayer: function (feature, latlng) {
    return L.circleMarker(latlng, geojsonMarkerOptions);
  }
}).addTo(map);

//add your geojson data to the layer
var xhr = new XMLHttpRequest();
xhr.open('GET', encodeURI("BFRO_bigfootA.geojson"));
xhr.onload = function() {
if (xhr.status === 200) {
    geojson.addData(JSON.parse(xhr.responseText));
  } else {
    alert('Request failed.  Returned status of ' + xhr.status);
  }
};
xhr.send();
```