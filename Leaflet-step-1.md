### Setting up the basics 

 :arrow_forward: Open your text editor.

 :arrow_forward: Create an empty file to make your basic HTML page. Copy the following into your file:

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

 :arrow_forward: Save the file in `yourDirectory` and call the file `index.html`.

 :arrow_forward: Change the title to “My first Leaflet map".

 :arrow_forward: Place a ‘div’ in the `<body>` 

``` html
<div id="map"></div>
```
The `<div>` is a kind of frame where our map will come! This frame does not contain anything yet and it is not even there yet. We will have to give it some dimensions in order to show content. We will specify the width and height with CSS, so the `<div>` can be seen. Later, we will give content to the `<div>` with JavaScript.

 :arrow_forward: Open a new file and save this as `main.css` in `yourDirectory`.

With CSS we will style our `<div>` object. In the `main.css` we will provide our "#map" selector with the rule height(and optional width).

 :arrow_forward: Copy this in your CSS file:

``` css
#map { 
  height: 500px; 
  width:100%;
} 
```
 :arrow_forward: Change the amount of pixels and/or percentage to the map size you prefer.

To link our CSS file with our HTML objects we will have to put a link in our HTML file. 

 :arrow_forward: Go back to your index.html file and put the link to your CSS file in the `<head>`.

``` html
<link rel="stylesheet" href="main.css"/>
```

Now we will add the JavaScrip Library Leaflet.js.

 :arrow_forward: Go to http://leafletjs.com/download.html to use the Hosted Version of Leaflet.

 :arrow_forward: Scroll down and copy the newest leaflet library release:

``` html
<link rel="stylesheet" href="https://unpkg.com/leaflet@1.0.3/dist/leaflet.css" />
<script src="https://unpkg.com/leaflet@1.0.3/dist/leaflet.js"></script>
```
 :arrow_forward: Place the `leaflet.css Link` in the `<head>` of your html file.

 :arrow_forward: Place the `leaflet.js script` library in the `<body>`. 


> **JS** *JavaScript libraries are often placed in the head. Though, it is best to place them as far as possible to the bottom of the body. This is much quicker while loading!*


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

 :arrow_forward: Put the following script in the body and save your index.html file. 

``` js
<script>
  //initialize the map         
  var map = L.map('map').setView([42.3600825, -71.0588801], 12);
  
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

:information_source: `var map =  L.map("map")` initializes the `map` variable and links it to our `<div id="map"></div>`. This will link the map content to the `<div>` content.

:information_source: `setView()` centres the map `([latitude, longitude], zoom level)`. The projection is Google Mercator. 

:information_source: Next we add our base-layer tiles. `L.tileLayer('http://...')` graps one from the internet. 

:information_source: `backgroundMap.addTo()` adds the tile layer to the map.


Now you have made your first web map!

 :arrow_forward: Open your index.html file in your browser!

Do you see your map? Great! 


> ###  :bangbang: you do not see a map? 
> Open the debugger 
>
> * Click with your right mouse button, choose : `Inspect Element`
> * Or Press F12
> 
> The debugger shows you the content of your page. But also logs any errors or comments! 
> Go to the tab `Web Console` to see if it reports anything useful for you.
> 
> Do you get:
> 
> `ReferenceError: L is not defined`
> 
> Then shuffle around the order in your script. Put the `leaflet.js script` above your custom script!


### Customizing

Practice with different tiles, coordinates and zoom levels to make your own base map. 

 :arrow_forward: Try to zoom your map to the place where you live or work! 

 :arrow_forward: Looking for a specific place to centre on? Find your coordinates here: [http://www.mapcoordinates.net/en](http://www.mapcoordinates.net/en)

 :arrow_forward: There are many different tile providers! Just copy their code given, replacing your own code starting from `L.tileLayer (... );` Try out some different styles. 

Another free tile provider is [maps.stamen.com](maps.stamen.com). These even provide 3 varieties:
 
   * http://tile.stamen.com/toner/{z}/{x}/{y}.png
   * http://tile.stamen.com/terrain/{z}/{x}/{y}.jpg
   * http://tile.stamen.com/watercolor/{z}/{x}/{y}.jpg

Or have a look at https://leaflet-extras.github.io/leaflet-providers/preview/ 

:arrow_right: Continue to [[Leaflet Step 2]]