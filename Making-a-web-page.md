### HTML

Hypertext Markup Language is used to structure content for web browsers. The simplest HTML page looks like this:

``` html
    <!DOCTYPE html>
    <html>
        <head>
            <title> My First HTML </title>
        </head>
        <body>
            <H1>Example</H1>
            <p>This is a really interesting paragraph.</p>
        </body>
    </html>
```

**Let's try this!**

1. Open your text editor.
2. Copy the previous code into an empty file to make your basic HTML page.
3. Save the file in `yourDirectory` and call the file `index.html`.
4. Open your index.html file with your browser.

[This](https://nieneb.github.io/html_example/) is what it should look like!

Some basic elements to know and recognize are:
    
`<head>` The `<head>` element is a container for all the head elements.
The `<head>` element can include a title for the document, scripts, styles, meta information, and more.

`<body>` The `<body>` tag defines the document's body.
The `<body>` element contains all the contents of an HTML document, such as text, hyperlinks, images, tables, lists, etc.
    
`<h1></h1>` to `<h6></h6>` are headings. `<h1>` defines the most important heading. `<h6>` defines the least important heading. 
`<p></p>` The `<p>` tag defines a paragraph.
`<div></div>` The `<div>` tag defines a division or a section in an HTML document.
`<a href=""></a>` The `<a>` tag defines a hyperlink, which is used to link from one page to another.

5. Try to add some more headers and text to your first HTML.

### Developer Tools

That sounds scary! But do not be afraid. The browser web inspector is going to be your best friend! Let's explore this. 

1. In your browser when you opened your html 
* Click with your right mouse button, choose : `Inspect Element`

or 

* Press F12

The web inspector shows you the content of your page and the current state of the DOM. 

2. Do you see the same content as we just made in our text editor?
3. Just have a look around. Nothing can happen!


### DOM

The Document Object Model refers to the hierarchical structure of HTML. Web browsers parse the DOM in order to make sense of a page’s content.

**But this webpage looks really boring!!**
True, so let´s continue with CSS. 

### CSS

Cascading Style Sheets are used to style the visual presentation of HTML pages. Every element of your HTML can be styled with CSS.

A simple CSS stylesheet looks like this:

```css
    body {
        background-color: blue;
        color: white;
    }
```

CSS styles consist of selectors and rules. Selectors identify the specific elements of your HTML to which styles will be applied. Examples of some rules:

    color: pink;
    background-color: yellow;
    margin: 10px;
    padding: 25px;

We connect selectors and rules using curly brackets:

```css
    p {
        font-size: 12px;
        line-height: 14px;
        color: white;
    }
```

CSS rules can be included directly within the head of a document, like so

```html
    <head>
        <style type="text/css">
            p {
                font-family: sans-serif;
                color: lime;
            }
        </style>
    </head>
```

or saved in an external file with a .css suffix, and then referenced in the document’s head:

```html
    <head>
        <link rel="stylesheet" href="style.css">
    </head>
```

**We will try this!**

1. Copy this style code into your index.html page.

```html
    <style type="text/css">
        body {
            background-color: blue;
            color: white;
        },
        p {
            font-family: sans-serif;
            color: lime;
        }
    </style>
```

2. Refresh your browser.
[This](https://nieneb.github.io/css_example/) is how it should look like.

3. Play around with the CSS and HTML. Make yourself a nice page! 
On https://www.w3schools.com/css/ you can find a great overview of all the possibilities with CSS.

### JavaScript

JavaScript is a dynamic scripting language that can instruct the browser to make changes to a page after it has already loaded.

Scripts can be included directly in HTML, between two script tags

```html
    <body>
        <script type="text/javascript">
            alert("Hello, world!");
        </script>
    </body>
```

or stored in a separate file, and then referenced somewhere the HTML (commonly in the head):

```html
    <head>
        <title>Page Title</title>
        <script type="text/javascript" src="myscript.js"></script>
    </head>
```

We will explain the JavaScript part, immediatly with Leaflet. Because we all came here to make interactive maps!

**Continue to [[Leaflet Step 1]]**