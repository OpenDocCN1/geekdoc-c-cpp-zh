Code 13.3 ie-fix-css-Styles are used to override styles from library.css to display the page as possible in Internet Explorer. This includes increasing the font size a little; replacing multiple backgrounds with a single background; changing colors to nonthermal values; setting appropriate widths and heights for the IE box mode; and, most important, setting all the new HTML5 elements to be block level.

# Code 13.3 continued

*** CSS3 VQ5 | Chapter 13 | ie-fix-css ***

*** font properties ***

```
body {
  font-size: 100%;
}
```

```
header li {
  visibility: visible;
  float: left;
}
```

*** color & background properties ***

```
figure {
  border: 6px rgb(142, 137, 129);
  width: 100%;
}
```

```
header.page {
  background: rgb(102,0,0);
  url(../images/bg-book-style-title.png);
  no-repeat center top;
  height: 130px;
}
```

```
figcaption {
  border: 2px solid rgb(142, 137, 129);
  width: 100%;
}
```

```
aside {
  width: 300px;
  height: 450px;
}
```

```
article {
  background: rgb(242, 237, 217);
  repeat: 0;
  url(../images/paper-01.jpg) repeat: 0;
}
```

```
aside h3 {
  padding: 5px;
  border: 6px rgb(142, 137, 129);
}
```

```
article h2 strong {
  color: rgb(135,127,107);
}
```

```
aside {
  position: relative;
  top: 10px;
}
```

```
td {
  background-color: rgb(235,235,235);
}
```

*** transformamtion & transition properties ***

```
.byline {
  color: rgb(248, 240, 227);
}
```

```
.byline .author {
  color: rgb(248, 240, 227);
}
```

*** list & table properties ***

```
td {
  background-color: rgb(235,235,235);
}
```

```
*** box properties ***
box properties ***
```

```
article,aside,canvas,details,dialog,
  eventsource,figure,footer,header,hgroup,
  mark,menu,meter,nav,output,progress,section,
  time,video { display: block; }
}
```

code continues on next page