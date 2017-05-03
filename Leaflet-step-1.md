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

4. Change the title to “My first Leaflet map".
5. Place a ‘div’ in the `<body>` 

``` html
<div id="map"></div>
```
This is where our map will come!

6. Open a new file and save this as `main.css` in `yourDirectory`. 
7. In the `main.css` we will provide your "map" with a height(and optional width). Copy this in your CSS file:

``` css
#map { 
  height: 300px; 
  width:100%;
} 
```
8. Change the amount of pixels and/or percentage to the map size you prefer.

9. Go back to your index.html file and put the link to your CSS file in the `<head>`.

``` html
<link rel="stylesheet" href="main.css"/>
```

10. Go to http://leafletjs.com/download.html to use the Hosted Version of Leaflet.
11. Scroll down and copy the newest leaflet library release:

``` html
<link rel="stylesheet" href="https://unpkg.com/leaflet@1.0.3/dist/leaflet.css" />
<script src="https://unpkg.com/leaflet@1.0.3/dist/leaflet.js"></script>
```
12. Place the `leaflet.css Link` in the `<head>` of your html file.
13. Place the `leaflet.js script` library in the `<body>`. 

> ***
> **JS** *JavaScript libraries are often placed in the head. Though, it is best to place them as far as possible to the bottom of the body. This is much quicker while loading!*
> ***

Now you will have:

``` html
<!doctype html>
<html>
  <head>
    <title>My first Leaflet map</title>  
    <link rel="stylesheet" href="https://unpkg.com/leaflet@1.0.3/dist/leaflet.css" />
    <link rel="stylesheet" href="main.css"/>
  </head>   
  <body>
    <H1>example</H1>
    <div id="map"></div>
    <script src="https://unpkg.com/leaflet@1.0.3/dist/leaflet.js"></script>
  </body>
</html>
```
The basics are done! 

### Adding a base layer

For a real map you need a base layer. This is the background of your map made out of png tiles, which are quick to load!

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

**Now you have made a map!**

* `var map =  L.map("map")` initializes the `map` variable and links it to our `<div id="map"></div>`.
* `setView()` centres the map `([latitude, longitude], zoom level)`. The projection is Google Mercator. 
* Next we add our base-layer tiles. `L.tileLayer('http://...')` graps one from the internet. 
* `backgroundMap.addTo()` adds the tile layer to the map.

2. **Open your index.html file in your browser!**

Do you see your map? Great! 

> ***
> ### If Not: Open the debugger 
>
> * Click with your right mouse button, choose : `Inspect Element`
> 
> or 
> 
> * Press F12
> 
> The debugger shows you the content of your page. But also logs any errors or comments! 
> Go to the tab `Web Console` to see if it reports anything useful for you.
> 
> Do you get:
> 
  > ReferenceError: L is not defined
> 
> Then shuffle around the order in your script. Put the `leaflet.js script` above your custom script!
> ***

### Customizing

Practice with different tiles, coordinates and zoom levels to make your own base map. 

1. Try to zoom your map to the place where you live or work! 
2. Looking for a specific place to centre on? Find your coordinates here: [http://www.mapcoordinates.net/en](http://www.mapcoordinates.net/en)
3. There are many different tile providers! Just copy their code given, replacing your own code starting from `L.tileLayer (... );`

> ***
> Another free tile provider is [maps.stamen.com](maps.stamen.com). These even provide 3 varieties:
> 
  > * http://tile.stamen.com/toner/{z}/{x}/{y}.png
  > * http://tile.stamen.com/terrain/{z}/{x}/{y}.jpg
  > * http://tile.stamen.com/watercolor/{z}/{x}/{y}.jpg
> 
> Or have a look at https://leaflet-extras.github.io/leaflet-providers/preview/ 
> *** 



Continue to [[Leaflet Step 2]]