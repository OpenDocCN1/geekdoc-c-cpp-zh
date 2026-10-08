+   - Through the jQuery object, you can access the built-in engine for visual effects. In the library, you find an effective engine for building custom animations, plus a few facilities for quickly implementing common effects such as fading and sliding.

+   - jQuery has strong Ajax support (based on the ajax function), through which you can control all aspects of a web request.

+   - Most nontrivial JavaScript code use some kind of client-side cache. You do not have to create your own, because jQuery provides one.

# Selectors and Filters

Just as the WHERE clause is the key for the SQL statement to select matching specified conditions, and filters are the essence ofjQuery to access DOM elements. With selectors, you can position to specific elements in the DOM. Filters specify additional conditions to include or exclude the element in the wrapped set as the result of the jQuery operation.

The jQuerySelectors.html file in your jQuerySamples project contains several sample queries. This file contains a table with bulleted lists in each cell, as shown in Figure 20-30.

Each button at the bottom of the page represents an operation based on a jQuery wrapped set. For example, the "First Album to Red" changes the first <li> in the page to have a red color with the following script:

```
function firstRed() {
  $(".lifirst").addClass("red");
}
```

In this sample, li is a selector (select all li elements in the page), and :first is a filter (select the first item from the selector). The combination of them results in "select the first li item in the page." The AddClass is a jQuery method that adds the specified CSS class to the wrapped set.

There are several selectors, as shown in Table 20-11.

![](bbox=[0.523, 0.291, 0.905, 0.613])

FIGURE 20-30: jQuerySelectors.html in action