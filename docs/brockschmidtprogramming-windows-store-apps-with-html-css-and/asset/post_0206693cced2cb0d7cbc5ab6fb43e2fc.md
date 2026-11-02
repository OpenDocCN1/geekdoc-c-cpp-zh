
## Grouping

When a ListView is supplied with a group data source in addition to its item data source, what changes for a custom layout is that the tree argument to the layout method will contain more than one item. Each item in tree, of course, is a single group that contains whatever items belong to that group. That is, we've been using code like this to look at the items:

```
var container = tree[0].itemsContainer;
```

but now we need to process the whole tree array instead. Scenarios 3 and 4 of the HTML ListView custom layout sample (again, the SDK sample) do this, as shown here from js/scenario3.js:

```javascript
layout: function (tree, changedRange, modifiedElements, modifiedGroups) {
    var offset = 0;

    var treeLength = tree.length;
    for (var i = 0; i < treeLength; i++) {
        this._layoutGroup(tree[i], offset);
        offset += tree[i].itemsContainer.items.length;
    }

    return WinJS.Promise.wrap();
},

// Private function that is responsible for laying out just one group
_layoutGroup: function (tree, offset) {
    var items = tree.itemsContainer.items;

    var itemsLength = items.length;
    for (var i = 0; i < itemsLength; i++) {
        // Get CSS class by item index
        var cssClass = this._itemInfo(i + offset);
        WinJS.Utilities.addClass(items[i], cssClass);
    }
}
```

All this is again a matter of adding CSS styles to various elements; the layout of the group headers themselves are defined by the headerTemplate element in html/scenario3.html and applicable styles in css/scenario3.css. As shown below, this is just a large character for each group (the groups are arranged vertically; I'm showing portions of each horizontally here):

![](img/0e8e4a2b6f953d3397e14e88cd5d8b4d_726_0.png)

In short, support for grouping isn't tied to the implementation of specific ILayout2 methods—it's primarily a matter of how you implement the layout method itself.

You can, of course, implement both grouping and virtualization together by including itemsFromRange, as we saw in the previous section. Scenario 4 of the sample demonstrates this by basically combining the code from scenarios 2 and 3.

## The Other Stuff

Let's now look at the remaining methods of ILayout2, most of which are demonstrated in scenario 4 of the Custom Layout Extras example, which is an extension of the minimum horizontal layout in scenario 2.

Some of these methods must return an object that contains an item index and a type (a value from WinJS.UI.ObjectType). This object doesn't have an assigned type, but looks like this:

```
return { type: WinJS.UI.ObjectType.item, index: itemIndex };
return { type: WinJS.UI.ObjectType.groupHeader, index: headerIndex };
```

The hitTest method should also include an insertAfterIndex, which indicates the actual insertion point of a moved item.

### Keyboard Support: getAdjacent

The ListView calls getAdjacent in response to the arrow keys as well as page up and page down, because the layout object is what knows how items are arranged in relation to one another. Without this method, the default behavior (as you can see in scenario 2) is that the right arrow, down arrow, and page down move the focus to the next item in the list, and left arrow, up arrow, and page up go to the previous item. (Home and End always go to the first and last item as expected.)

In this grid layout, however, we want the up, down, page up, and page down to work by rows (one row or three rows at a time). We implement getAdjacent, then, which accepts an item object (which contains index and type properties as in the return object) and a WinJS.Utilities.Key, and returns an object describing the next item to get the focus. (If you simply return an object with index set to item.index + 1 or item.index - 1, for forward and backward keys, respectively, and type: WinJS.UI.ObjectType.item, you'll duplicate the default behavior.)

In our case we need to determine how many items are in a row. This is fairly straightforward. Remember the site object we get through initialize? It contains a viewportSize property whose width tells us the width of the ListView. If we divide this by the item width—and it's best to have a property on the layout object through which the app can specify this as a fixed size—we get the items per row. Because this value will change only when the layout is recomputed, we can do this in the layout method:

```
layout: function() {
    this._itemsPerRow = Math.floor(this._site.viewportSize.width / this._itemWidth);
    this._totalRows = Math.floor(this._site.itemCount._value / this._itemsPerRow);

    //We don't need to do anything else.
    return WinJS.Promise.as();
},
```

Assuming that we have an itemWidth property on the layout that's been set appropriately for the real item size (content size + borders, etc.), we can implement getAdjacent as follows. Here, page up and page down move three rows at a time, and up/down arrow one row:

```
getAdjacent: function (item, key) {
    var Key = WinJS.Utilities.Key;
    var index = item.index;
    var curRow = Math.floor(index / this._itemsPerRow);
    var curCol = index % this._itemsPerRow;
    var newRow;

    //The ListView is gracious enough to ignore our return index if it's out of bounds,
    //so we don't have to check for that here.

    switch (key) {
        case Key.rightArrow:
            index = index + 1;
            break;

        case Key.downArrow:
            index = index + this._itemsPerRow;
            break;

        case Key.pageDown:
            //If we page down past the last item, this will go to the last item
            newRow = Math.min(curRow + 3, this._totalRows);
            index = curCol + (newRow * this._itemsPerRow);
            break;

        case Key.leftArrow:
            index = index - 1;
            break;

        case Key.upArrow:
            index = index - this._itemsPerRow;
            break;

        case Key.pageUp:
            newRow = Math.max(curRow - 3, 0);
            index = curCol + (newRow * this._itemsPerRow);
            break;
    }

    return { type: WinJS.UI.ObjectType.item, index: index };
},
```

With this, we will get good keyboard navigation within the layout. Note the comment that the ListView will ignore invalid index values, so we don't have to sweat over validating what we return.

moves an item dragged within the list to this index. Note that `insertAfterIndex` should be set to -1 to insert at the beginning of the list.

With `hitTest` in place, the `dragOver` method is then called whenever the index from `hitTest` changes. It receives the x/y coordinates of the drag operation (along with an object called *`dragInfo`* that's for the ListView's internal use as all its members start with `_`, indicating 'don't touch'). The method doesn't have a return value, so its whole purpose is to give your layout an opportunity to visually indicate the result of a drop. For example, you can highlight the insertion point, show a little wiggle room in the layout (the built-in layouts move hit-tested items by 12px), or whatever else you want. You then use `dragLeave`, of course, to reset that indicator. (If you want to look at what the built-in layouts do for `dragOver`, look in the `ui.js` file of WinJS for the `_layoutCommon_dragOver` function.)

In the example (still in scenario 4) I just rotate the item at the drop point a little (see Video 8-3) and make sure to clear that transform on `dragLeave`:

```js
dragOver: function (x, y, dragInfo) {
    //Get the index of the item we'd be dropping on
    var index = this._indexFromCoordinates(x, y);

    console.log("dragOver on index = " + index);

    //Get the element and scale it a little (like a button press)
    var element = this._site.tree[0].itemsContainer.items[index];
    element && this._addAnimateDropPoint(element);
    this._lastRotatedElement && this._clearAnimateDropPoint(this._lastRotatedElement);
    this._lastRotatedElement = element;
},

dragLeave: function () {
    console.log("dragLeave");
    if (this._lastRotatedElement) {
        this._clearAnimateDropPoint(this._lastRotatedElement);
        this._lastRotatedElement = null;
    }
},

_addAnimateDropPoint: function (element) {
    element.style.transition = "transform ease 167ms";
    element.style.transform = "rotate(-20deg)";
},

_clearAnimateDropPoint: function (element) {
    element.style.transition = "";
    element.style.transform = "";
}
```

With this, the ListView will automatically take care of moving items around in the data source without any other special handling. In the example, I've added identification numbers to each of the items in the list so that you can see the effects.
