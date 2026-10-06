14.2 layout—Creates columns when applied to 14.1. In addition to a simple CSS reset, the layout code sets the width of the total page, along with the width and padding of each column (for a fixed horizontally page must equal the overall width of the page), and then floats the three columns so that they float next to each other than stacking.

```
*** CSS53 VQ | Chapter 14 | layout.css ***
```

```
/* CSS Simple Reset
------------------------------------------------------
*/

*{margin:0;padding:0;border:outline:0;line-height:1.4em;vertical-align:baseline;text-decoration:none;}
```

```
/* Layout */

header, nav, section, article, aside, footer {
display: block; /* Sets HTML5 elements to */
overflow: hidden; /* Fixes Child Float Problem */ }
```

```
body {
  background-color: rgb(153,153,153);
  font: normal 1em/1.4em Perpetua, Constantia, times, "times new roman", serif;
}
```

```
header.site, section, footer.site {
width: 980px;
clear: both;
margin: 0 auto;
}
```

```
section {
background: rgb(204,204,204);
}
```

```
nav, article, aside {
float: left;
}
```

```
nav {
width: 235px;
_width: 205px;
}
```

```
article {
padding: 0px;
background: rgb(255,255,255);
width: 470px;
width: 430px;
}
```

```
aside {
ppadding: 0px;
width: 135px;
width: 95px;
}
```

```
ul {
list-style: none;
margin: 1em;
}
```