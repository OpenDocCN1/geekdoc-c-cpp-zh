# Code 10.12 continued

-moz-border-radius: 5px;
border-radius: 5px;

```
figcaption {
display: block;
padding: 10px;
border-top: 2px solid rgba(142, 137, 129, 0.5);
padding: 10px;
}
aside {
display: block;
width: 200px;
height: 400px;
overflow: auto;
float: right;
margin: 10px;
-webkit-border-top-left-radius: 20px;
-webkit-border-bottom-left-radius: 20px;
-moz-border-radius: 20px 0 20px;
border-radius: 20px 0 20px;
padding: 25px;
}
```

To set each side's padding value separately, you can type from one to four values.

+   - One sets the padding for all four sides.
- Two sets the padding for the top/bottom and left/right sides.
- Three values set the padding for the left/right sides (the same), and the bottom padding.
- Four values set the padding for each side in this order: top, right, bottom, and left.

+   3. As with margins, padding can also be set on all four sides of the box (top, right, bottom, and left).
padding-right: 10px;

```
footer {
width: 100%;
clear: both;
}
```

```
h1 {
margin: 0 20px 10px 10%;
padding-top: 10px;
```

```
article h2 {
border-top: 2px solid rgba(142, 137, 129, 0.5);
pading: 20px;
```

```
article nav h2 {
border-top: none;
padding: 0;
```

```
aside h3 {
border: 1em double rgb(142, 137, 129);
-webkit-border-radius: url(../images/border-02.png) 27 round;
-moz-border-radius: url(../images/border-02.png) 27 round;
```

```
.byline {
margin: 0 10% 10px 20%;}
```

> TIP If there is no border or background-color behind the element, the margin will have the same visual as padding, and you won't run into the issues Chapter 13, "Fixing the Internet Explorer Model")

![](bbox=[0.548, 0.563, 0.933, 0.755])

Code 10.12 apply to Code 10.1: With padding added, the whole design finally comes, opening up the page and making it easier to scan and navigate.

Box Properties 275