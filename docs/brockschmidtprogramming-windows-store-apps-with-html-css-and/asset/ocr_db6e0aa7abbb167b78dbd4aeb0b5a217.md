is the same thing using the following code in JavaScript:

```
listView.layout = new <layout_class>({ <option1>: <value1>, <option2>, <value2>, ... });
```

And that's it! Running the sample with this layout now in portrait mode, as shown in Figure B-2, we see that the result is a simple vertically oriented ListView, with each item's height determined naturally by its item template. What's impressive about this is that it took almost no code to effectively create the equivalent of a variable-size vertical ListView, something that was amazingly difficult to do in WinJS 1.0 (and was one of the most requested features for WinJS 2.0).

The reason for this is that the ListView is building up a DOM tree of div elements for the items in the list, but otherwise it leaves it to the layout to define their positioning. Because our layout doesn't do anything special, we end up with the default layout behavior of the app host. Because div elements use block layout by default (position: static), they are just rendered vertically like any other markup.

![](bbox=[0.1, 0.5, 0.95, 0.85])

FIGURE B-2 Scenario 1 of the HTML ListView custom layout sample, shown in portrait view so that we can see more of the ListView. The templates are defined in html\scenario1.html are also shown here. Because each item in the list is rendered in a div, and a div uses block layout in the rendering engine, the items render vertically by default.