
### Extra data
Now we will load the vd data and visualize it as circles. (from the leaflet starter workshop)

1. Put the vd.geojson file in your js folder
2. Copy the next script
	
	~~~~
	// create a new SVG group element
	var layerVD = svg.append('g');
	
	d3.json("js/vd.geojson", function(data){                  
	//Create a circle for each city
		layerVD.selectAll("circle")
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
				.attr("r", 5)
				.style("fill", "blue")
				.style("opacity", 0.75);
	});
	~~~~              
				   
3. Change the colours and play around with the style attributes! 

### Do you want to learn more?
* Book: interactive data visualization Scott Murray. Or on-line via http://alignedleft.com/tutorials/d3/about
* follow tutorials on YouTube for example of D3.vienno
