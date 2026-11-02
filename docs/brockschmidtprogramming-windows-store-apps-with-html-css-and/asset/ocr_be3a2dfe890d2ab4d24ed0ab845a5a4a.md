```
```js
var cssClassSizeMap = {
    statusItemSize: { height: 90 }, // plus 10 pixels to incorporate the margin-top
    photoItemSize: { height: 260 }  // plus 10 pixels to incorporate the margin-top
};
```
```

Again, be very, very clear that such constructs are entirely specific to the custom layout and have no impact whatsoever on the ListView itself except as the layout implements methods like `layout` and `itemsFromRange`. In the sample, `layout` just uses this to cache various information about the items to improve performance. `itemsFromRange`, for its part, uses that cached size information to translate pixels to indexes for items. Here's how it's implemented in js/scenario2.js:

```
```js
itemsFromRange: function (firstPixel, lastPixel) {
    var totalLength = 0;

    // Initialize firstIndex and lastIndex to be an empty range
    var firstIndex = 0;
    var lastIndex = -1;

    var firstItemFound = false;

    var itemCacheLength = this._itemCache.length;
    for (var i = 0; i < itemCacheLength; i++) {
        var item = this._itemCache[i];
        totalLength += item.height;

        // Find the firstIndex
        if (!firstItemFound && totalLength >= firstPixel) {
            firstIndex = item.index;
            lastIndex = firstIndex;
            firstItemFound = true;
        } else if (totalLength >= lastPixel) {
            // Find the lastIndex
            lastIndex = item.index;
            break;
        } else if (firstItemFound && i === itemCacheLength - 1) {
            // If we are at the end of the cache and we have found the firstItem,
            // the lastItem is in the range
            lastIndex = item.index;
        }
    }

    return { firstIndex: firstIndex, lastIndex: lastIndex };
},
```
```

The most important thing to keep in mind with `itemsFromRange` is to make it fast. This is why the sample employs a caching strategy, which would become essential if you had a large data source.

Along these lines, be careful about the properties you access on HTML elements—some of them can trigger layout passes especially if other layout-related properties have been changed. That is, dimensional properties, to be accurate, must make sure that the layout is up to date before values can be returned, and clearly you don't want this to happen inside a method like `itemsFromRange`.