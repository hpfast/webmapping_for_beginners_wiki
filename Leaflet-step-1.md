## My first web-map! 

1. Open your text editor.
2. Create an empty file to make your basic HTML page. Copy the following into your file:

	~~~~
	<!DOCTYPE html>
	<html>
		<head>
			<title> My title </title>
		</head>
		<body>
			<H1>Example</H1>
		</body>
	</html>
	~~~~

3. Save the file in `yourDirectory` and call the file `index.html`.


4. Go to http://leafletjs.com/download.html to use the Hosted Version of Leaflet.
5. Scroll down and copy the newest leaflet library release:

	~~~~
	<link rel="stylesheet" href="https://unpkg.com/leaflet@1.0.3/dist/leaflet.css" />
	
	<script src="https://unpkg.com/leaflet@1.0.3/dist/leaflet.js"></script>
	~~~~

6. Place the `leaflet.css Link` in the `<head>` of your html file.
7. Place the `leaflet.js script` library in the `<body>`. 
	* JavaScript libraries are often placed in the head. Though, it is best to place them as far as possible to the bottom of the body. This is much quicker while loading! 

8. Open a new file and save this as ‘main.css’ in a new folder in `yourDirectory` called: `yourDirectory/style’. 
9. You can also create the following folders here: ‘images’ and ‘js’. Now you have:
	* /yourDirectory/index.html
	* /yourDirectory/style/main.css
	* /yourDirectory/images/
	* /YourDirectory/js/

10. Open your ‘index.html’ file and put the link to your CSS file in the `<head>`.

	~~~~
	<link rel="stylesheet" href=“style/main.css"/>
	~~~~

11. Change the title to “My first Leaflet map".
12. Place a ‘div’ in the `<body>` 

	~~~~
	<div id="map"></div>
	~~~~

13. The basics are done! Provide your "map" always with a height(and optional width). This you do in the main.css.

	~~~~
	#map { height: 300px; width:100%;} 
	~~~~

14. Change the amount of pixels and/or % to the map size you prefer.

Now you will have:

	~~~~
	<!doctype html>
	<html>
		<head>
			<title>My first Leaflet map</title>  
			<link rel="stylesheet" href="https://unpkg.com/leaflet@1.0.3/dist/leaflet.css" />
			<link rel="stylesheet" href="style/main.css"/>
		</head>   
		<body>
			<H1>example</H1>
			<div id="map"></div>
		<script src="https://unpkg.com/leaflet@1.0.3/dist/leaflet.js"></script>
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