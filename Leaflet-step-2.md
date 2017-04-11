### Markers, circles and polygons
Add custom markers, circles and polygons to your map. (for example your home address). At least, choose coordinates which are on your map.

1. Add the following to your map:

	~~~~
	var marker = L.marker([51.5, -0.09]).addTo(map);
	~~~~

2. Add another 4 markers. (friends, places you lived or visited?). Note: do give the ‘var’ another name every time. Example:

	~~~~
	var monique = L.marker([52.070, 4.300]).addTo(map);
	~~~~

3. Provide the markers with a pop-up. For monique we add the following pop-up:

	~~~~
	var popup = "Write your pop up text here";
	monique.bindPopup(popup); 
	~~~~


4. How to place a circle on the map, use your own coordinates:

	~~~~
	var circle = L.circle([51.508, -0.11], 500, {
		color: 'red',
		fillColor: '#f03',
		fillOpacity: 0.5
	}).addTo(map);
	~~~~

5. Connect all previous markers with a polygon. Use all previous coordinates and combine them in the right order.

	~~~~
	var polygon = L.polygon([
		 [51.509, -0.08],
		 [51.503, -0.06],
		 [51.51, -0.047]
	]).addTo(map);
	~~~~


6. Your script should look like the following. Also check the debugger in the browser if everything is correct: F12

	~~~~
	<script>
	//initialize the map
	var map = L.map('map').setView([52.18, 5.5308], 11);
	
	//Create baselayer - tiles
	var backgroundMap = L.tileLayer('http://{s}.basemaps.cartocdn.com/light_all/{z}/{x}/{y}.png', {
		attribution: '<a href="http://openstreetmap.org">OpenStreetMap</a>contributors, <a href="http://creativecommons.org/licenses/by-sa/2.0/">CC-BY-SA</a>',
		maxZoom: 19
	});
	
	backgroundMap.addTo(map);
	
	//Add markers
	var monique = L.marker([52.070, 4.300]);
	monique.addTo(map);
	
	var miranda = L.marker([53.201, 5.799]);
	miranda.addTo(map);
	
	var barbel = L.marker([52.351, 4.620]);
	barbel.addTo(map);
	
	var bea = L.marker([51.560, 5.091]);
	bea.addTo(map);
	
	//Add pop-ups
	var popup = "Monique lives in Den Haag.";
	monique.bindPopup(popup);
	
	var popup1 = "Barbel lives in Heemstede.";
	barbel.bindPopup(popup1)
	
	var popup2 = "Miranda lives in Leeuwarden.";
	miranda.bindPopup(popup2);
	
	var popup3 = "Bea lives in Tilburg.";
	bea.bindPopup(popup3);
	
	//add a circle
	var circle = L.circle([52.156, 5.387], 4500, {
		color: 'red',
		fillColor: '#f03',
		fillOpacity: 0.5
	}).addTo(map);  
	
	//add a polygon   
	var polygon = L.polygon([
		[53.201, 5.799],
		[52.351, 4.620],
		[52.070, 4.300],
		[51.560, 5.091]
	]).addTo(map);
	</script>
	~~~~

### geoJson-tilelayer
geoJson is the standard data type to create web maps with. You can add this data as another map layer.

* Do you want to know more about geojson have a look at https://en.wikipedia.org/wiki/GeoJSON
* ! geoJson mostly works on a 'local webserver', check: https://github.com/mrdoob/three.js/wiki/How-to-run-things-locally

1. Place the vd.geojson file in your js folder
2. Plave vd.png in your img folder
3. Copy the following script and have a look at your map

	~~~~
	//geojson without jQuery with xhr define icon first
	
	var vdIcon = L.icon({
		iconUrl: "images/vd.png",
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
	xhr.open('GET', encodeURI("js/vd.geojson"));
	xhr.onload = function() {
	if (xhr.status === 200) {
			geojson.addData(JSON.parse(xhr.responseText));
		} else {
			alert('Request failed.  Returned status of ' + xhr.status);
		}
	};
	xhr.send();
	~~~~

Continue to [[Leaflet step 3]]