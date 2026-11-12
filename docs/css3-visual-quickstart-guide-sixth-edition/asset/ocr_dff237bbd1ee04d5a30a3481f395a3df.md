Code 12.2 Added to transition-properties.css— When applied to Code 12.1, several transformations give the aside a jaunty angle and break up the grid containing the images B. Notice that four lines of code are required for maximum cross-browser compatibility.

```
/*** transition-properties.css ***/
aside {
	-webkit-transform: rotate(-2deg);
	-moz-transform: rotate(-2deg);
	-ms-transform: rotate(-2deg);
	-o-transform: rotate(-2deg);
	transform: rotate(-2deg);
}
div.gallery figure {
	-webkit-transform-origin: left 25%;
	-moz-transform-origin: left 25%;
	-o-transform-origin: left 25%;
	transform-origin: left 25%;
}
div.gallery figure#f1 {
	-webkit-transform: scale(.75)
		rotate(10deg);
	-moz-transform: scale(.75)
		rotate(10deg);
	-o-transform: scale(.75) rotate(10deg);
	transform: scale(.75) rotate(10deg); }
div.gallery figure#f3 {
	-webkit-transform: scale(.75)
		rotate(3deg);
	-moz-transform: scale(.75)rotate(3deg);
	-o-transform: scale(.75) rotate(3deg);
	transform: scale(.75) rotate(3deg); }
```

![](bbox=[0.06, 0.6, 0.45, 0.88])

B At the top of the page, the aside title is at a slight angle.

# To add a 2D transformation to an element:

+   1. Add the transform property:
+   -webkit-transform:
+   -moz-transform:
+   -ms-transform:
+   -o-transform:
+   transform:

The exact order is not important, although standard CSS should always come last (Code 12.2).

![](bbox=[0.5, 0.43, 0.91, 0.88])

C When expanded, the angle is more noticeable.