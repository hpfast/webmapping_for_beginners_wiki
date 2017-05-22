
### Extra data
Now we will load the Squatch Watch Data and visualize it as circles on our map. (from the leaflet starter workshop)

:arrow_forward: Download the dataset from https://github.com/NieneB/Webmapping_for_beginners/tree/gh-pages/data

:arrow_forward: Place the BFRO_bigfootA.geojson or BFRO_bigfootb.geojson file in `yourDirectory`.

:arrow_forward: Copy the following script and have a look at your map.
	
	~~~~
	// create a new SVG group element
	var layerYeti = svg.append('g');
	
	d3.json("BFRO_bigfoot_A.geojson", function(data){                  
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
	~~~~              

:arrow_forward: Change the map location so we see all of the Squatch Watch Data in the US.

``` js
var projection = d3.geoMercator()
    .center([ -100, 45 ])
    .translate([ w/2, h/2 ])
    .scale([ w/2 ]);
```
:arrow_forward: Change the colours and play around with the style attributes! 


### Data Driven Styling

Using the data for styling and effects.

~~~
.style("fill", function(d){
	if (d.properties.styleUrl = '#a') {
		return "red"
	} else return "blue"
})
~~~



:arrow_right: Continue to [[Hosting on Github]] to put your maps online! Or do the [[D3 advanced]] turorial.