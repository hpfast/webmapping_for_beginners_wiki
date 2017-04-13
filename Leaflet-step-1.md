### Setting up the basics 

1. Open your text editor.
2. Create an empty file to make your basic HTML page. Copy the following into your file:

``` html
<!DOCTYPE html>
  <html>
    <head>
      <title> My title </title>
    </head>
  <body>
    <H1>Example</H1>
  </body>
</html>
```

3. Save the file in `yourDirectory` and call the file `index.html`.
4. Go to http://leafletjs.com/download.html to use the Hosted Version of Leaflet.
5. Scroll down and copy the newest leaflet library release:

``` html
<link rel="stylesheet" href="https://unpkg.com/leaflet@1.0.3/dist/leaflet.css" />
<script src="https://unpkg.com/leaflet@1.0.3/dist/leaflet.js"></script>
```

6. Place the `leaflet.css Link` in the `<head>` of your html file.
7. Place the `leaflet.js script` library in the `<body>`. 
	* JavaScript libraries are often placed in the head. Though, it is best to place them as far as possible to the bottom of the body. This is much quicker while loading! 

8. Open a new file and save this as `main.css` in a new folder in `yourDirectory` called: `yourDirectory/style`. 
9. You can also create the following folders here: `images` and `js`. Now you have:
	* /yourDirectory/index.html
	* /yourDirectory/style/main.css
	* /yourDirectory/images/
	* /yourDirectory/js/

10. Open your index.html file and put the link to your CSS file in the `<head>`.

``` html
<link rel="stylesheet" href=“style/main.css"/>
```

11. Change the title to “My first Leaflet map".
12. Place a ‘div’ in the `<body>` 

``` html
<div id="map"></div>
```

13. The basics are done! Provide your "map" always with a height(and optional width). This you do in the main.css.

``` css
#map { height: 300px; width:100%;} 
``` 

14. Change the amount of pixels and/or % to the map size you prefer.

Now you will have:

``` html
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
```

### Adding a base layer

For a real map you need a base layer. This is the background of your map, made out of png tiles, which are quick to load!

1. Put the following script in the body and save your index.html file. 

``` js
<script>
	//initialize the map         
	var map = L.map('map').setView([52.18, 5.5308], 11);
	
	//Create baselayer - tiles         
	var backgroundMap = L.tileLayer('http://{s}.basemaps.cartocdn.com/light_all/{z}/{x}/{y}.png',
		{
		attribution: '<a href="http://openstreetmap.org">OpenStreetMap</a>contributors, <a href="http://creativecommons.org/licenses/by-sa/2.0/">CC-BY-SA</a>',
		maxZoom: 19
		}
	);
	
	backgroundMap.addTo(map);
</script>
``` 

2. Now you have made a map!
	* var map =  L.map("map"): initializes the "map" variable
	* setView() centres the map (latitude, longitude, zoom level). The projection is Google Mercator. 
	* Next we add our base-layer tiles. `L.tileLayer()` graps one from the internet. 
	* backgroundMap.addTo() adds the tile layer to the map.

**Open your index.html file in your browser!**
Do you see your map? Great! 

If not:
### Open the debugger 

* Click with your right mouse button, choose : `Inspect Element`

or 

* Press F12

The debugger shows you the content of your page. But also logs any errors or comments! 
Go to the tab `Web Console` to see if it reports anything useful for you.

Do you get:

	ReferenceError: L is not defined

Then shuffle around the order in your script. Put the `leaflet.js script` above your custom script!


### Customizing

5. Practice with different tiles, coordinates and zoom levels to make your own base map. For example, try to zoom in to the place where you live or work! 

3. Looking for a specific place to centre on? Find your coordinates here:
http://www.mapcoordinates.net/en

4. Another free tile provider is maps.stamen.com. These even provide 3 varieties:

	* http://tile.stamen.com/toner/{z}/{x}/{y}.png
	* http://tile.stamen.com/terrain/{z}/{x}/{y}.jpg
	* http://tile.stamen.com/watercolor/{z}/{x}/{y}.jpg

Or have a look at https://leaflet-extras.github.io/leaflet-providers/preview/ 
There are many different tiles to use! Just copy the code given at the top, replacing your own code starting from `L.tileLayer (... );`


Continue to [[Leaflet Step 2]]