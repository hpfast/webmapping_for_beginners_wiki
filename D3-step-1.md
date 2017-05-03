### Setting up the basics 

1. Open your text editor 
2. Start with a basic HTML page
3. Save the file in a `yourDirectory` and call the file `index.html`.

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

4. Open a new file and save this as `main.css` in `yourDirectory`. 
5. Go back to your index.html file and put the link to your CSS file in the `<head>`.

``` html
<link rel="stylesheet" href="main.css"/>
```

6. Go to [d3js.org](https://d3js.org/). Scroll down and download the newest release (`d3.v4.min.js`). Or use the snippet provided below. Because we already have utf-8 stated in the `<head>` we do not have to specify it in the script. (utf-8 makes sure all diacritical marks are placed right)

``` html
<script src="https://d3js.org/d3.v4.min.js"></script>
```

**JS** *JavaScript libraries are often placed in the head. Though, it is best to place them as far as possible to the bottom of the body. This is much quicker while loading!*

7. Change the title to “My first map in D3”. 

Now your file will look like:

``` html
<!doctype html>
<html lang="nl">
<html>
	<head>
		<meta charset="utf-8">
		<title>My first map in D3</title> 
		<link rel="stylesheet" href="main.css"/> 
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

1. Replace “your code goes here” with:

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
2. Some Javascript explenation:

*The double slashes `//` mark a Single line comment. Any text between `//` and the end of the line will be ignored by JavaScript (will not be executed). JavaScript comments can be used to explain JavaScript code, and to make it more readable.*

*The `;` at the end of every statement tells the computer that the statement has ended.*

*`var` stands for variable. Variables store data so that they can be used later on in the program.

3. What did you do?

* First you created to variables with the width and height of your map (named w and h) for your browser screen(in pixels)

``` js
//Width and height
var w = 500;
var h = 300;
```

* Next we chose our projection of the map. Mercator is the most common.
* The `centre` we set with longitude and latitude. 
* `translate`, in this way, takes care that our map is in the centre of the area.
* `scale` is the zoom-level  

``` js
//Define map projection
var projection = d3.geoMercator()
	.center([30, 40])
	.translate([ w/2, h/2 ])
	.scale([ w/7 ]);
```
				
* When the projection is created we can transform our geographic data to SVG with the help of `D3.geoPath` 
	
``` js
//Define path generator
var path = d3.geoPath()
	.projection(projection);
``` 

* Next, we create our 'canvas' where we will display our map. You create a variable and give it a name, for example *svg*. 
* `d3` is a call to the functions of D3. 
* `select`, selects one element of the DOM, in this case the `<body>`. 
* `append`, appends a SVG to the 'canvas' called *svg* 
* next we also provide the `attr` (attributes), width and height.
	
``` js
//Create SVG
var svg = d3.select("body")
	.append("svg")
	.attr("width", w)
	.attr("height", h);
``` 

### Data
To 'bind' your data to the DOM is the next step. With D3 you can connect data like .csv or in our case .json files.

1. Place the file landen.json in `yourDirectory`.
2. Copy the following script, below the previous script (index.html).

``` js
// create a new SVG group element
var layerLanden = svg.append('g');

//Load in GeoJSON data
d3.json("landen.json", function(json) {
	//Bind data and create one path per GeoJSON feature
	layerLanden.selectAll("path")
		 .data(json.features)
		 .enter()
		 .append("path")
		 .attr("d", path);
}); 
```

3. Check in your browser if you see a world map.
4. Have a look at https://github.com/d3/d3-3.x-api-reference/blob/master/Geo-Projections.md for different projections.
5. You can also play around with the projection, centre and zoom level. 
6. For example, try to zoom in on the Netherlands!

``` js
var projection = d3.geoMercator()
	.center([4, 52])
	.translate([ w/2, h/2 ]
	.scale(1000);
```


If you do not see anything:
### Open the debugger 

* Click with your right mouse button, choose : `Inspect Element`

or 

* Press F12

The debugger shows you the content of your page. But also logs any errors or comments! 
Go to the tab `Web Console` to see if it reports anything useful for you.

Do you get:

	...

Continue to [[D3 Step 2]]