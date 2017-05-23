### Adding a data driven legend

:arrow_forward: Let's add the legend to the map:

	//Create Legend
	var legend = d3.select("body")
		.append("div")
		.attr("class", "legend")
		.attr("width", "100%")
		.attr("height", "50px");

:arrow_forward: Add data to the legend so it is actually there!

	legend.selectAll("rect")
		.data(color.domain())
		.enter()
		.append("rect")
		.attr("class", "rect")
		.style("width", ((w/8)*100)/w+"%")
		.style("background-color", function(d){
			return color(d)
		})
		.text(function(d){
			return d + "%"
		})
		.style("color", "#fff")
		.style("text-align","center")
	    .style("vertical-align", "bottom")
	    .style("font-weight", "bold")
	    .style("font-size", "18px");


## Do some JavaScript for getting the unique values.

// Array of parties
	for(var key in json.features[0].properties){
		attributen.push(key);
	}
	var partij_lijst = attributen.slice(15,attributen.length -16);


### Adding a TimeScale graph

