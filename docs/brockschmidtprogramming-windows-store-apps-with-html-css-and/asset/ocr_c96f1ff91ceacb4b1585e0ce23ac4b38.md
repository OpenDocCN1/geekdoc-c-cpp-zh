# Grouping

When a ListView is supplied with a group data source in addition to its item data source, what changes for a custom layout is that the tree argument to the layout method will contain more than one item. Each item in tree, of course, is a single group that contains whatever items belong to that group. That is, we've been using code like this to look at the items:

```
var container = tree[0].itemsContainer;
```

but now we need to process the whole tree array instead. Scenarios 3 and 4 of the HTML ListView custom layout sample (again, the SDK sample) do this, as shown here from js/scenario3.js:

```
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
_layoutGroup = function (tree, offset) {
    var items = tree.itemsContainer.items;

    var itemsLength = items.length;
    for (var i = 0; i < itemsLength; i++) {
        // Get CSS class by item index
        var cssClass = this._itemInfo(i + offset);
        WinJS.Utilities.addClass(items[i], cssClass);
    }
}
```
```

All this is again a matter of adding CSS styles to various elements; the layout of the group headers themselves are defined by the headerTemplate element in html/scenario3.html and applicable styles in css/scenario3.css. As shown below, this is just a large character for each group (the groups are arranged vertically; I'm showing portions of each horizontally here):

![](bbox=[0.12, 0.85, 0.88, 0.95])