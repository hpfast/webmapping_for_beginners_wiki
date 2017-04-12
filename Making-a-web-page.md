### HTML

Hypertext Markup Language is used to structure content for web browsers. The simplest HTML page looks like this:

    <html>
        <head>
            <title>Page Title</title>
        </head>
        <body>
            <h1>Page Title</h1>
            <p>This is a really interesting paragraph.</p>
        </body>
    </html>

### DOM

The Document Object Model refers to the hierarchical structure of HTML. Each bracketed tag is an element, and we refer to elements’ relative relationships to each other in human terms: parent, child, sibling, ancestor, and descendant. In the HTML above, body is the parent element to both of its children, h1 and p (which are siblings to each other). All elements on the page are descendants of html.

Web browsers parse the DOM in order to make sense of a page’s content.

### CSS

Cascading Style Sheets are used to style the visual presentation of HTML pages. A simple CSS stylesheet looks like this:

    body {
        background-color: white;
        color: black;
    }

CSS styles consist of selectors and rules. Selectors identify specific elements to which styles will be applied:

    h1          /* Selects level 1 headings              */
    p           /* Selects paragraphs                    */
    .caption    /* Selects elements with class "caption" */
    #subnav     /* Selects element with ID "subnav"      */

Rules are properties that, cumulatively, form the styles:

    color: pink;
    background-color: yellow;
    margin: 10px;
    padding: 25px;

We connect selectors and rules using curly brackets:

    p {
        font-size: 12px;
        line-height: 14px;
        color: black;
    }

D3 uses CSS-style selectors to identify elements on which to operate, so it’s important to understand how to use them.

CSS rules can be included directly within the head of a document, like so

    <head>
        <style type="text/css">
            p {
                font-family: sans-serif;
                color: lime;
            }
        </style>
    </head>

or saved in an external file with a .css suffix, and then referenced in the document’s head:

    <head>
        <link rel="stylesheet" href="style.css">
    </head>

### JavaScript

JavaScript is a dynamic scripting language that can instruct the browser to make changes to a page after it has already loaded.

Scripts can be included directly in HTML, between two script tags

    <body>
        <script type="text/javascript">
            alert("Hello, world!");
        </script>
    </body>

or stored in a separate file, and then referenced somewhere the HTML (commonly in the head):

    <head>
        <title>Page Title</title>
        <script type="text/javascript" src="myscript.js"></script>
    </head>

### Developer Tools

Be familiar with your browser’s developer tools. In a WebKit browser (like Safari or Chrome), you can open the web inspector, which looks something like this:

![web_inspector]()

While “View Source” shows you the original HTML source of the page, the web inspector shows you the current state of the DOM. This is useful because your code will modify DOM elements dynamically. In the web inspector, you can watch elements as they change. You’ll also use the JavaScript console for debugging. See more on debugging HTML, CSS, and JavaScript with the web inspector and console.

### SVG

D3 is at its best when rendering visuals as Scalable Vector Graphics. SVG is a text-based image format. Meaning, you can specify what an SVG image should look like by writing simple markup code, sort of like HTML tags. In fact, SVG code can be included directly within any HTML document. Web browsers have supported the SVG format for years (except for Internet Explorer), but it never quite caught on, until now.

Here’s a little circle that I just coded into this page:

    <svg width="50" height="50">
        <circle cx="25" cy="25" r="22"
         fill="blue" stroke="gray" stroke-width="2"/>
    </svg>

You’re not required to use SVG with D3, but you’ll soon find that SVG provides a range of visual opportunities that aren’t possible with regular HTML elements.

### GeoJSON



**Continue to [[Leaflet Step 1]]**