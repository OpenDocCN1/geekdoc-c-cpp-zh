# # Handling Size Changes

Designing an app for different sizes, as noted in the previous section, is a matter of thinking through the user experience for full screen landscape and portrait views, partial landscape views (landscape aspect ratio), partial portrait views (narrow views down to 500px with a portrait aspect ratio), and possibly narrow views below 500px. We did this in Chapter 2 with the *Here My Am!* app. Once you get to the implementation details, however, handling size changes in each view of an app is very much the same story as *responsive design* for web pages and generally doesn't need to be more complicated than that.

Responsive design has two parts. First are those things you can handle declaratively in CSS:

+   - Place all size-independent and default styles in CSS outside of any media queries. Apps typically specify styles for their preferred full screen orientation, such as landscape, as the default.

+   - For size-specific styles, use media queries with appropriate combinations of orientation, min-width, max-width, min-height, and max-height media features to isolate different layout cases. For example:

```
```css
/* Default styles here */

@media screen and (orientation: landscape) and (max-width: 1024px) {
    /* Styling for smaller landscape layouts */
}

@media screen and (orientation: portrait) and (min-width: 500px) {
    /* Styling for portrait aspect ratios (width/height < 1)*/
}

@media screen and (orientation: portrait) and (max-width: 499px) {
    /* Styling for narrow portrait aspect ratios (width/height < 1)*/
}

@media screen and (orientation: landscape)
and (min-width: 1600px) and (min-height: 1200px) {
    /* Styling for landscape layouts on larger displays */
}

@media screen and (orientation: portrait)
and (min-width: 1200px) and (min-height: 1600px) {
    /* Styling for portrait layouts on larger displays */
}
```
```

+   - The CSS for each size typically changes placement of elements within CSS grids, the flow directions within a CSS flexbox, and element display styles (to show or hide those elements).

+   - In CSS there are also variables for the viewport height and viewport width: *vh* and *vw*. You can prefix these with a percentage number—for example, 100vh is 100% of the viewport height, and 3.5vw is 3.5% of the viewport width. These variables can also be used in CSS `calc` expressions.