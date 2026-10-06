# TABLE 12.3 Transform-Origin Keywords

| Value |
| --- |
| left |
| right |
| top |
| bottom |
| center |

+   3. Add more transformations as needed.
transform: scale(.75) rotate(3deg);
You can include multiple transformation values separated by a space.
4. Specify the transformation origin, if it is not the center of the element.
-webkit-transform-origin: 0, 25%;
-moz-transform-origin: 0, 25%;
-o-transform-origin: 0, 25%
transform-origin: 0, 25%;

# Do Browser Extensions Ever Go Away?

Yes, browser extensions eventually go away. After a browser implements the standard W3C syntax of a property, the browsers generally support the extension for the next two versions of the browser, although this is by no means a hard and fast rule. This is why—if standard CSS syntax has been defined—it is best to include it at the bottom of the list of browser extension properties to ensure that it's the version that is used, if supported.

By default, all transformations use the center of the element as the origin. Thus, a rotate transform will rotate around the middle of the element.
To change this, add the transform() property with one or two values for the X and Y location of the origin (Table 12.2) as a percentage, or as keyword. If you specify only a single value, it used for both X and Y. Positive values move the origin up and to the left of the element, whereas negative values move the origin down and to the right of the center

# 3D transformations

As of this writing, 3D transitions are supported only in Safari and Chrome, although that can rapidly change as new versions of Firefox are released. As a result, I don't advocate the use of 3D transitions except in cases where you know the only browser being used is one that supports these properties—for example, in iOS applications or pages created for iPhone, iPod touch, or iPad display. That said, because this is a standard under development by the W3C, you should also include the standard CSS3 syntax for future compatibility.

Transformation and Transition Properties 311