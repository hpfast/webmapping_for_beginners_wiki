## Leaflet.js

Leaflet is an open-source JavaScript library for interactive web maps. It's lightweight, simple, and flexible, and is probably the most popular open-source mapping library at the moment. Leaflet is developed by Vladimir Agafonkin (currently of MapBox) and other contributors. 

![Leaflet-logo](img/leaflet-logo.png)

Leaflet creates "Slippy" maps with raster tiled base layers, user interaction like panning and zooming, and feature layers that you supply. It handles various basic tasks like converting data to map layers and mouse interactions, and it's easy to extend with plug-ins. It will also work well across most types of devices. 

> ### JavaScript Library 
> Including a JavaScript library in your code is like copying and pasting someone else's code into yours. You have access to everything in that library. In our case, it's a bunch of cool tools to make web maps and give them familiar functionality.

## Web maps

Web maps are made up of many small, square images called tiles. These tiles are typically 256x256 pixels and are placed side-by-side in order to create the illusion of a very large seamless image. A big advantage: all these little tiles load way faster than one big map! This kind of map is  called a "Slippy" map. 

![slippy map](http://maptime.io/anatomy-of-a-web-map/images/tiles-loading.gif)

Each zoom level has its own set of tiles. Zoom level 0 has 1 tile for the world. With each additional zoom level, the number of tiles increases exponentially. So zoom level 1 has 4 tiles for the world. Zoom level 2 has 16 tiles for the world ect. 

![Zoom levels](img/slippy_maps.jpeg)

As you can see, map tiles are static raster images on the web. These tiles need to live somewhere on the web page. They need to know when to load and they need to react when you click or drag. Leaflet is a JavaScript library that allows us to do just that.

In [[Leaflet step 1]] we will set up the basics to show a standard background map with Leaflet.

In [[Leaflet step 2]] we will add markers, circles and polygons to our map.

In [[Leaflet step 3]] we will add a GeoJSON file containing geo-spatial data to our map.


## Preparation

:arrow_forward: On your computer create a directory for yourself, where we can work in today. For example:

	/home/niene/Documents/MyFirstWebMap_Leaflet

We'll save everything we make and download today in this directory. During this workshop it is referred to as `yourDirectory`.

## Let's start!
:arrow_right: If you are not that comfortable with HTML, CSS and JavaScript yet, this **[[Making a web page ]]** tutorial will help you along!

:arrow_right: If you already know some HTML, CSS and JavaScript, you can start immediately with the tutorial at **[[Leaflet step 1 ]]** and read through the HTML explanations. 



