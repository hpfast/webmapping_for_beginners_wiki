### Extra data
Now we will load the Squatch Watch Data and visualize it as circles on our map. (from the leaflet starter workshop)

:arrow_forward: Download the dataset from https://github.com/NieneB/Webmapping_for_beginners/tree/gh-pages/data

:arrow_forward: Place the All_BFRO_Reports_points.geojson file in `yourDirectory`.

:arrow_forward: Copy the following script and have a look at your map.

``` js
// create a new SVG group element
var layerYeti = svg.append('g');

d3.json("All_BFRO_Reports_points.geojson", function(data){
	//Create a circle for each city
	layerYeti.selectAll("circle")
		.data(data.features)
		.enter()
		.append("circle")
		.attr("cx", function(d) {
			//[0] returns the first coordinate (x) of the projected value
			return projection(d.geometry.coordinates)[0];
		})
		.attr("cy", function(d) {
			//[1] returns the second coordinate (y) of the projected value
			return projection(d.geometry.coordinates)[1];
		})
		.attr("r", 2)
		.style("fill", "blue")
		.style("opacity", 0.75);
});
```
What did we do?

:information_source: First we added an extra layer called layerYeti to our svg and group all its paths in 'g'.

:information_source: Then, we call the GeoJSON file and put it through the function. Creating a circle for every feature in the data.

```js
d3.json("All_BFRO_Reports_points.geojson", function(data){
	//Create a circle for each city
	layerYeti.selectAll("circle")
		.data(data.features)
		.enter()
		.append("circle")
```
:information_source: The circles need a location, so assigning it a "cx" and "cy" attribute is required. We use the geometry coordinates for that of course, and our projection object, which we created before and also used for our world map! the function takes all the features, calls is 'd' and by accessing d.geometry.coordinates[0] we will get the x coordinate of each point! The same is done for the y coordinate of course. 

```js
.attr("cx", function(d) {
	//[0] returns the first coordinate (x) of the projected value
	return projection(d.geometry.coordinates)[0];
})
.attr("cy", function(d) {
	//[1] returns the second coordinate (y) of the projected value
	return projection(d.geometry.coordinates)[1];
})
```

:information_source: The circles will have a radius of 2 pixels and styled with a fill color blue and a opacity of 75%.
```js
.attr("r", 2)
.style("fill", "blue")
.style("opacity", 0.75);
```

Now work on our map a bit:

:arrow_forward: Change the map location so we see all of the Squatch Watch Data in the US.

``` js
var projection = d3.geoMercator()
	.center([ -100, 45 ])
	.translate([ w/2, h/2 ])
	.scale([ w/2 ]);
```
:arrow_forward: Maybe you want to make the map bigger now? 

``` js
//Width and height
	var w = 1000;
	var h = 800;
```

### Data Driven Styling

The Squatch Watch data is categorized in classes. The sightings get a classification label for how trustworthy the sighting was! For example : Class A reports involve clear sightings in circumstances where misinterpretation or misidentification of other animals can be ruled out with greater confidence. Incidents where a possible Squatch was observed at a great distance or in poor lighting conditions and incidents in any other circumstance that did not afford a clear view of the subject are considered Class B reports.

We can use these attributes for styling the data! To see what attributes are available in the data set we can do 2 things.

1. Open the GeoJSON file with your text editor.
2. Let the browser print your data set in the console. 

Let's try both!

:arrow_forward: 1. Open the GeoJSON file with your text editor. This might take a little while because the dataset is quite big. 
This is what it looks like:

``` json
{
"type": "FeatureCollection",
"crs": { "type": "name", "properties": { "name": "urn:ogc:def:crs:OGC:1.3:CRS84" } },
"features": [
{ "type": "Feature", "properties": { "name": "June 2000", "styleUrl": "#a", "styleHash": "72e6f3ff", "styleMapHash": { "normal": "#anormal", "highlight": "#ahighlighted" }, "description": "\r\n          Report 637: Campers' encounter just after dark in the Wrangell - St. Elias National Park and PreserveClass A; Cordova-McCarthy CountyClick for details(Location look wrong?)", "timestamp": "2000\/06\/16 12:00:00", "stroke-width": null, "fill": null, "fill-opacity": null, "visibility": null }, "geometry": { "type": "Point", "coordinates": [ -142.9, 61.5, 100.0 ] } },
{ "type": "Feature", "properties": { "name": " 1995", "styleUrl": "#a", "styleHash": "72e6f3ff", "styleMapHash": { "normal": "#anormal", "highlight": "#ahighlighted" }, "description": "\r\n          Report 2917: Family observes large biped from carClass A; Prince of Wales CountyClick for details(Location look wrong?)", "timestamp": "1995\/05\/15 12:00:00", "stroke-width": null, "fill": null, "fill-opacity": null, "visibility": null }, "geometry": { "type": "Point", "coordinates": [ -132.7982, 55.1872, 100.0 ] } },  
....
]
}
```

:arrow_forward: 2. Put a `console.log(data);` line in your code after the call for the data to view your dataset in the browser. So you get:

``` js
//Call the geojson data
d3.json("All_BFRO_Reports_points.geojson", function(data){
	
	//view the data
	console.log(data);

	//Create a circle for each city
	layerYeti.selectAll("circle")
```

:arrow_forward: Go to the browser, refresh and open the debugger. Go to the `Web console` tab. Here you will see your Object printed.

> * Click with your right mouse button, choose : `Inspect Element`
> * Or Press F12

:arrow_forward: Click the object and go through the nice drop down view of your dataset to explore what it contains! 

The GeoJSON FeatureCollection contains Features which each exist out of properties and a geometry. 
In our case the properties contain:

	- name
	- styleUrl
	- styleHash
	- StyleMapHash
	- description
	- timestamp
	- stroke-width
	- fill
	- fill-opacity
	- visibility

A lot of it is not usable, but is used by the BFRO themselves. We will now focus on the styleUrl property, because these contain the classification labels! 

Let's try to give each point a different colour according to their classification label.

:arrow_forward: Replace the `.style("fill", "blue")` attribute with the following code. 

``` js
.style("fill", function(d){
	if (d.properties.styleUrl == "#a") {return "red"}
	else if (d.properties.styleUrl == "#b") {return "blue"}
	else { return "yellow"}
})
```

:information_source: `function(d)`

:arrow_right: Continue to [[D3 step 3]] if you feel really confident! If you are almost running out of time it might be nice to spend the last bit of the workshop on putting your map on-line! Go to the [[Hosting on Github]] to learn how! 
