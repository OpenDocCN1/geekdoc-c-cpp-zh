# # Using Background Shorthand to Add Multiple Background Images and Gradients

| Value | | | | | | |
|---|---|---|---|---|---|---|
| <background-color> | ● | ● | ● | ● | ● | ● |
| <background-image> | ● | ● | ● | ● | ● | ● |
| <background-position> | ● | ● | ● | ● | ● | ● |
| <background-size> | ● | ● | ● | ● | ● | ● |
| <background-repeat> | ● | ● | ● | ● | ● | ● |
| <background-attachment> | ● | ● | ● | ● | ● | ● |
| Multiple backgrounds | 9 | ● | ● | ● | ● | ● |
| SVG backgrounds | 9 | ● | ● | ● | ● | ● |

The background shorthand property (Table 7.14) allows you to define the background image and color for an entire page or individual element, rolling many of the background properties into a single quick and compressed declaration. From a coding standpoint, this method is preferable because it uses less space, but it requires that you remember the purpose of each of the values in the list.

```
/*** color-background-properties.css ***/
body {
background: rgb(76,76,76) url(../images/chrome/dark-victorian.jpg) repeat 0 0;
}
header.page {
background: url(../images/book/book-spine-title.png) no-repeat right top,
rgb(102,0,0) url(../images/chrome/bg-book-book-spine.jpg) repeat-x 0 0; }
article {
background: url(../images/chrome/embelish-01.png) no-repeat right top,
rgb(242, 237, 217) url(../images/chrome/paper-01.jpg) repeat 0 0;
}
footer {
display: block;
padding: 1.5em;
background: rgb(153,153,153);
background: -webkit-linear-gradient(top, rgba(0,0,0,0), rgba(0,0,0,1));
background: -moz-linear-gradient(top, rgba(0,0,0,0), rgba(0,0,0,1));
background: -ms-linear-gradient(top, rgba(0,0,0,0), rgba(0,0,0,1));
background: -o-linear-gradient(top, rgba(0,0,0,0), rgba(0,0,0,1));
background: linear-gradient(to top, rgba(0,0,0,0), rgba(0,0,0,1)); }
figure {
background: rgb(242, 237, 217) url(../images/chrome/paper-01.jpg) repeat 0 0; }
```