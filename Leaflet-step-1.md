# Workshop 1

## My first web-map! 

### Leaflet 
With leaflet you can make interactive web maps for all devices. Leaflet is made by Vladimir Agafonkin and is an open source JAvaScript library. So free to use. If you already know some HTML, CSS and JavaScript, you can start immediately and read through the HTML explanations. If you are not that comfortable with it yet, this tutorial will help you along!

### What do you need?
* A bit of knowledge about HTML, DOM, CSS and JavaScript is useful. A short explanation can be found here: http://alignedleft.com/tutorials/d3/fundamentals
* A text editor for all your code, for example Brackets or Sublime text
* internet
* your browser, for example chrome, which has a nice debugger. 

### Your first map
1. open your text editor 
2. start with a basic HTML page
3. Save the file in a new folder and call the file index.html

	~~~~
	<!doctype html>
	<html lang="nl">
	
	<html>
	 	<head>
				<meta charset="utf-8">
	    	<title>basic HTML</title>  		 
	 	</head>
		
	 	<body>
	    	<H1>Example</H1>
	 	</body>
	</html>
	~~~~

4. Go to http://leafletjs.com/download.html
5. Scroll down and copy the newest leaflet library release.

	~~~~
	<link rel="stylesheet" href="https://unpkg.com/leaflet@1.0.1/dist/leaflet.css" />
	
	<script src="https://unpkg.com/leaflet@1.0.1/dist/leaflet.js"></script>
	~~~~
	
		
6. Place the leaflet.css in the head
7. Place the leafletjs library in the body. 
	* JavaScript libraries are often placed in the head. Though, it is best to place them as far as possible to the bottom of the body. This is much quicker while loading! 

8. Open a new file and save this as ‘main.css’ in a new folder called: ‘style’. The style folder is placed in the same folder as where your index.html file is saved. 
9. You can also create the following folders here: ‘images’ and ‘js’. 
10. Open your ‘index.html’ file and put the link to your CSS file in the *head*

	~~~~
	<link rel="stylesheet" href=“style/main.css"/>
	~~~~

11. Change the title to “My first Leaflet map".
12. Place a ‘div’ in the body 

	~~~~
	<div id="map"></div>
	~~~~

13. The basics are done! Provide your "map" always with a height(and optional width). This you do in the main.css

	~~~~
	#map { height: 300px; width:100%;} 
	~~~~
 
14. Change the amount of pixels and/or % to the map size you prefer.

	~~~~
	<!doctype html>
	<html lang="nl">
	<html>
	 	<head>
			<meta charset="utf-8">
	    	<title>My first Leaflet map</title>  
			<link rel="stylesheet" href="https://unpkg.com/leaflet@1.0.1/dist/leaflet.css" />
			<link rel="stylesheet" href="style/main.css"/>
		</head>   
	 	<body>
	     	<H1>example</H1>
				<div id="map"></div>
				<script src="https://unpkg.com/leaflet@1.0.1/dist/leaflet.js"></script>
	 	</body>
	</html>
	~~~~

### Base layer	

For a real map you need a base layer. This is the background of your map, made out of png tiles, which are quick to load!

1. Put the following script in the body

	~~~~
		<script>
			//initialize the map         
			var map = L.map('map').setView([52.18, 5.5308], 11);
			
			//Create baselayer - tiles         
			var achtergrondkaart = L.tileLayer('http://{s}.basemaps.cartocdn.com/light_all/{z}/{x}/{y}.png',
			 	{
	    		attribution: '<a href="http://openstreetmap.org">OpenStreetMap</a>contributors, <a href="http://creativecommons.org/licenses/by-sa/2.0/">CC-BY-SA</a>',
	    		maxZoom: 19
				}
			);
			
			achtergrondkaart.addTo(map);
		</script>       
	~~~~

2. Now you have made a map.
	* var map =  L.map("map"): initializes the "map" variable
	* setView() centres the map (latitude, longitude, zoom level). The projection is Google Mercator. 
	* Next we add our base-layer tiles. For example from OpenStreetMap. 
	* addTo() adds the layer to the map
	

3. Looking for a specific place to centre on? Find your coordinates here:  
http://www.mapcoordinates.net/en		


4. Another free tile provider is maps.stamen.com. These even provide 3 varieties:
Or have a look at https://leaflet-extras.github.io/leaflet-providers/preview/ 

	* http://tile.stamen.com/toner/{z}/{x}/{y}.png
	* http://tile.stamen.com/terrain/{z}/{x}/{y}.jpg
	* http://tile.stamen.com/watercolor/{z}/{x}/{y}.jpg


5. Practice with different tiles, coordinates and zoom levels to make your own base map.


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
	var achtergrondkaart = L.tileLayer('http://{s}.basemaps.cartocdn.com/light_all/{z}/{x}/{y}.png', {
	    attribution: '<a href="http://openstreetmap.org">OpenStreetMap</a>contributors, <a href="http://creativecommons.org/licenses/by-sa/2.0/">CC-BY-SA</a>',
	    maxZoom: 19
	});
	
	achtergrondkaart.addTo(map);
	
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

### Tips			
* Learn basic HTML, CSS and JavaScript. For example at codecademy: https://www.codecademy.com/learn/web
* Do you want to use a special font? check ‘google fonts’
* Other nice exercise can be found at http://maptimeboston.github.io/leaflet-intro/
* Read the on line book 'leaflet tips and tricks, interactive maps made easy' by Malcolm Maclean. https://leanpub.com/leaflet-tips-and-tricks
* On Youtube watch films about web cartography geoJson and Leaflet of Ian Muehlenhaus. https://www.youtube.com/playlist?list=PLOlUoOtyTOXilBfrGanBziU738fyJdFqn
