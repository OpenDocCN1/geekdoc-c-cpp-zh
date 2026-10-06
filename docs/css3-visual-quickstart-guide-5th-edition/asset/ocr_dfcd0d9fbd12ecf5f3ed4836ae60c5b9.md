# To transform an element in three dimensions

+   1. Add the transform style property to your CSS declarations and specify the style.
-webkit-transform-style: flat;
transform-style: flat;
Add transform-style to the elements being transformed (Code 12.3), which allows you to specify which children elements should be set flat against the parent element or transformed separately in their own 3D spaces (Table 12.4).

+   2. Add the perspective style property to your CSS declarations and specify the perspective value.
-webkit-perspective: 500;
perspective: 500;
Perspective works like the transform() value described in this chapter but is used to apply a perspective to an element children (Table 12.5).

Code 12.3 transformation-properties.css—When applied to Code 12.1, it replaces the transform styles from Code 12.2 with Webkit-only 3D transforms. Other browsers will still look like this:

```
*** CSS VS | Chapter 12 | transform-properties.css ***

aside;
-webkit-transform: rotate(-2deg);
-moz-transform: rotate(-2deg);
-o-transform: rotate(-2deg);
transform: rotate(-2deg);

div.gallery figure {
width:
-webkit-transform-origin: left 25%;
-moz-transform-origin: left 25%;
-o-transform-origin: left 25%;
transform-origin: left 25%;
-webkit-transform-style: flat;
transform-style: flat;
-webkit-perspective: 5000;
perspective: 5000;
-webkit-perspective-origin: 25% 25%;
perspective-origin: 25% 25%;
-webkit-backface-visibility: visible;
backface-visibility: visible;
}
```

```
#f1
-webkit-transform: perspective(250)
+ scale3d(75,5,1) rotate3d(5,4,2,-10)
-moz-transform: scale(.75) rotate(10deg)
-o-transform: scale(.75) rotate(10deg);
transform: scale(.75) rotate(10deg);
```

```
#f2
-webkit-transform: perspective(250)
+ scale3d(5,7,1.5) rotate3d(3,-10,8,-18)
-moz-transform: scale(.75) rotate(-8deg);
```

| Value | Compatibility |
| --- | --- |
| flat | S3.1, C5, CSS3 |
| preserve-3d | S3.1, C5, CSS3 |

| Value | Compatibility |
| --- | --- |
| <number> | S3.1, C5, CSS3 |
| none | S3.1, C5, CSS3 |

code continues on next page