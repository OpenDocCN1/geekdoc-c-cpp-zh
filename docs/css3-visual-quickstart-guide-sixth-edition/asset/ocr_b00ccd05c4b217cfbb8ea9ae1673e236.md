Code 14.10 large.css contains adaptive styles for larger devices. Since Chapters 11–13 were built with a large screen in mind, I’m importing those styles into large.

```
/* *** Large Device Styles ***/
@import url(".../css/box-properties.css");
@import url(".../css/visual-formatting-properties.css");
@import url(".../css/transformation-transition-properties.css");
@import url(".../css/design-interface.css");

h1 {
    font-size: 5em;
}
nav.toc {
    color: rgba(0,0,0,.75);
}
```

Code 14.11 print.css includes some simple styles to make the page better for printing, as seen in Chapter 3.

```
/* *** For Print ***/

body {
    padding: 1em;
    color: rgb(0,0,0);
    background: white url(../chapters/alice23a.gif) no-repeat 0 0;
    padding: 200px 0 0 175px;
}

header.page, article {
    margin: 1em 0;
    background: none;
}
}

h1,h2,h3 { color: black; }
h2.chaptertitle { color: red; }
h2 cite { color: black; }

p { font: normal 12pt/2 Constantia, palatino, times, "times new roman", serif;
    text-indent: 3em; }

nav { display: none; }
```