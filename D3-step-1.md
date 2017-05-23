In D3 step 1 we will set up the basics to show a simple map with D3.

### Setting up the basics 

 :arrow_forward: Open your text editor.

 :arrow_forward: Start with a basic HTML page.

 :arrow_forward: Save the file in a `yourDirectory` and call the file `index.html`.

``` html
<!doctype html>
<html>
  <head>
    <meta charset="utf-8">
    <title>basic HTML</title> 
  </head>
  <body>
    <h1>Example</h1>
  </body>
</html>
```

:arrow_forward: Go to [d3js.org](https://d3js.org/). Scroll down and download the newest release (`d3.v4.min.js`). Or use the snippet provided below. 

> Because we already have utf-8 stated in the `<head>` we do not have to specify it in the script. (utf-8 makes sure all diacritical marks are placed right)

``` html
<script src="https://d3js.org/d3.v4.min.js"></script>
```

> **JS** *JavaScript libraries are often placed in the head. Though, it is best to place them as far as possible to the bottom of the body. This is much quicker while loading!*

:arrow_forward: Change the title to “My first map in D3”. 

Now your file will look like:

``` html
<!doctype html>
<html lang="nl">
<html>
  <head>
    <meta charset="utf-8">
    <title>My first map in D3</title> 
  </head>
  <body>
    <H1>Example</H1>
    <script src="//d3js.org/d3.v4.min.js"></script> 
    <script> your code goes here </script>
  </body>
</html>
```
The basics are done! 

### Setting up the map canvas

:arrow_forward: Replace “your code goes here” with:

``` js
<script> 
  //Width and height
  var w = 500;
  var h = 300;

  //Define map projection
  var projection = d3.geoMercator()
    .center([ 30, 40 ])
    .translate([ w/2, h/2 ])
    .scale([ w/4 ]);

  //Define path generator
  var path = d3.geoPath()
    .projection(projection);

  //Create SVG
  var svg = d3.select("body")
    .append("svg")
    .attr("width", w)
    .attr("height", h);
</script>
```

> Some JavaScript explanation:
> 
> *The double slashes `//` mark a Single line comment. Any text between `//` and the end of the line will be ignored by JavaScript (will not be executed). > JavaScript comments can be used to explain JavaScript code, and to make it more readable.*
> 
> *The `;` at the end of every statement tells the computer that the statement has ended.*
> 
> `var` *stands for variable. Variables store data so that they can be used later on in the program.

What did you do?

:information_source: First you created to variables with the width and height of your map (named w and h) for your browser screen(in pixels)

``` js
//Width and height
var w = 500;
var h = 300;
```

:information_source: Next we chose our projection of the map. Mercator is the most common.

:information_source: The `centre` we set with longitude and latitude. 

:information_source: `translate`, in this way, takes care that our map is in the centre of the area.

:information_source: `scale` is the zoom-level  

``` js
//Define map projection
var projection = d3.geoMercator()
  .center([30, 40])
  .translate([ w/2, h/2 ])
  .scale([ w/7 ]);
```

:information_source: When the projection is created we can transform our geographic data to SVG with the help of `D3.geoPath` 
  
``` js
//Define path generator
var path = d3.geoPath()
  .projection(projection);
``` 

:information_source:  Next, we create our 'canvas' where we will display our map. You create a variable and give it a name, for example *svg*. 

:information_source:  `d3` is a call to the functions of D3. 

:information_source:`select`, selects one element of the DOM, in this case the `<body>`. 

:information_source: `append`, appends a SVG to the 'canvas' called *svg* 

:information_source:  next we also provide the `attr` (attributes), width and height.
  
``` js
//Create SVG
var svg = d3.select("body")
  .append("svg")
  .attr("width", w)
  .attr("height", h);
``` 

### Adding Data
To 'bind' your data to the DOM is the next step. With D3 you can connect data like .csv or in our case a GeoJSON file. We will use a GeoJSON with the country shapes of the whole world!


:arrow_forward: Download the world dataset from https://github.com/NieneB/Webmapping_for_beginners/tree/gh-pages/data

:arrow_forward: Place the world.geojson file in `yourDirectory`.

:arrow_forward: Copy the following script, below the previous script (index.html).

``` js
// create a new SVG group element
var layerWorld = svg.append('g');

//Load in GeoJSON data
d3.json("world.json", function(json) {
  //Bind data and create one path per GeoJSON feature
  layerWorld.selectAll("path")
     .data(json.features)
     .enter()
     .append("path")
     .attr("d", path);
}); 
```

:arrow_forward: Check in your browser if you see a world map.

> ###  :bangbang: you do not see a map? 
> Open the debugger 
>
> * Click with your right mouse button, choose : `Inspect Element`
> * Or Press F12
> 
> The debugger shows you the content of your page. But also logs any errors or comments! 
> Go to the tab `Web Console` to see if it reports anything useful for you.
> 
> Do you get something like this:
> 
> `Uncaught SyntaxError: missing ) after argument list. index.html:19`
> 
> Then something is wrong in your code! This specific error means a `)` bracket is missing on line 19 of our script! 
> Try to fix your error and reload your page. 

:arrow_forward: Play around with the projection, centre and zoom level.

:arrow_forward: Have a look at https://github.com/d3/d3-3.x-api-reference/blob/master/Geo-Projections.md for different projections.

> Projection
> 
> Projections are what we call the mathematical equations that do the trick of turning the world into some flat shape that fits on a printout or a computer screen. It’s a messy task to do, this transformation - there’s no way to smoosh the world onto a screen without distorting it in some way. You either lose  direction, or relative size, or come out with something very weird looking.

![projection](img/projections.jpg)


:arrow_forward: For example, try to zoom in on the Netherlands!

``` js
var projection = d3.geoMercator()
  .center([4, 52])
  .translate([ w/2, h/2 ])
  .scale(1000);
```

:arrow_right: Continue to [[D3 Step 2]]