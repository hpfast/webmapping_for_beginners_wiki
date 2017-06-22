In Leaflet step 3 we will add a GeoJSON file containing geo-spatial data to our map.

### GeoJSON

[GeoJSON](http://geojson.org/) is the standard data type to create web maps with. You can add this data as another map layer.
The geodata that we want to add will be a GeoJSON file. JSON stands for JavaScript Object Notation. GeoJSON is a format for encoding a variety of geographic data structures.

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

The GeoJSON format specification can be found [here](http://geojson.org/) and [here](https://tools.ietf.org/html/rfc7946).

### Let's add the Bigfoot Sightings Data to our map!

We prepared a dataset for you that contains the viewing sites of bigfoot! The dataset is downloaded on the 3th of May 2017 from the [BFRO](https://www.bfro.net/) database. The BFRO is the only scientific research organization exploring the bigfoot mystery. Data is collected from 1995 till now. We pre-processed their data and exported it to a geojson file. If you want to know more about the Database history or the classification of the data have a look at the [BRFO documentation](https://www.bfro.net/GDB/classify.asp).


For inspiration: the following map is was also made from this dataset.

![bigfoot](http://thumbnails.visually.netdna-cdn.com/SquatchWatch92YearsofBigfootSightingsintheUSandCanada_523b7482cc497.png)


:arrow_forward: Download this [dataset](https://github.com/NieneB/Webmapping_for_beginners/blob/gh-pages/data/All_BFRO_Reports_points.geojson). 

:arrow_forward: Have a look at the file in your browser. Do you see how it is build up?

:arrow_forward: Right click: `Save Page As...`

:arrow_forward: Place the All_BFRO_Reports_points.geojson file in `yourDirectory`.


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


## Local server


If we want to add our own spatial data to our map, we need to run a local server.


## The code 

:arrow_forward: Copy the following script and have a look at your map.

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
xhr.open('GET', encodeURI("All_BFRO_Reports_points.geojson"));
xhr.onload = function() {
if (xhr.status === 200) {
		geojson.addData(JSON.parse(xhr.responseText));
	} else {
		alert('Request failed.  Returned status of ' + xhr.status);
	}
};
xhr.send();
```


### Running a local server




:arrow_right: Continue to [[Introduction D3]] or do the [[Leaflet Advanced assignments]]

