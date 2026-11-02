| Method | Description |
|---|---|
| `hitTest`, `dragOver` | If the ListView’s `itemsReorderable` is true, these are called when an item is dragged over the ListView. `hitTest` specifically determines when an item is at a particular (x,y) coordinate; `dragOver` (which receives the coordinates and a `dragInfo` object) is the signal for the layout to open up upon drop space for the item being dragged. |
| `setupAnimations`, `executeAnimations` | Called when it’s the right time to configure and execute animations, typically in response to movement of items in the ListView. Neither method has arguments. |

Fortunately, the ListView magnanimously allows you to implement only those parts of a layout class that you really need and ignore the rest, as it will fill the rest in with no-ops. We call this a “pay for play” mode. In the following table, the required method, `initialize`, is shaded in orange, the recommended methods in green (to support the most flexibility depending on your scenario), and truly optional methods in blue:

| Layout capability | Applicable methods |
|---|---|
| minimal | `initialize` (plus `uninitialize` if there’s any cleanup work) |
| non-vertical layout | Above plus `layout` |
| virtualization support | Above plus `itemsFromRange` |
| keyboard support | Add `getAdjacent` |
| drag and drop visual indicators (general) | Add `dragLeave` |
| reordering and positional drag and drop indicators | Add `hitTest`, `dragOver` (both are required together) |
| animations | Add `setupAnimations`, `executeAnimations` |

All this means again that the most basic custom layout object need only support `initialize` and possibly `uninitialized`, which will produce a vertical layout by default. To do a horizontal or nonlinear layout you’ll need the layout method, and then you can add others as you want to support additional features. Let’s now look at a number of examples.

# Minimal Vertical Layout

Our first example is scenario 1 of the [HTML ListView custom layout sample](#), whose data source (of ice cream flavors once again!) is a `WinJS.Binding.List` defined in js/data.js and accessed through the `Data.list` and `Data.groupedList` variables.

The custom layout object in scenario 1 is named `SDKSample.Scenario1.StatusLayout` and is created with `WinJS.Class.define` (js/scenario1.js):

```
WinJS.Namespace.define("SDKSample.Scenario1", {
    StatusLayout : WinJS.Class.define(function (options) {
        this._site = null;
        this._surface = null;
    },
    {
        // This sets up any state and CSS layout on the surface of the custom layout
        initialize: function (site) {
            this._site = site;
            this._surface = this._site.surface;

            // Add a CSS class to control the surface level layout
            WinJS.Utilities.addClass(this._site.surface, "StatusLayout");
```