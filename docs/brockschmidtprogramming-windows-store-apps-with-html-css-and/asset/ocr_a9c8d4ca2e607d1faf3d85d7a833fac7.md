The items, as noted in the table of adapter methods, are returned in the form of an object with the `IFetchResult` interface. Unlike the others we've seen, this one contains only properties, where `items` is the most important as it contains the item data (objects with `IItem`). Here's how the sample builds the fetch result: for each item in the HTTP response, it creates a data object (that can contain whatever information you want) and pushes it into an array called `results`:

```
```javascript
for (var i = 0, itemsLength = items.length; i < itemsLength; i++) {
    var dataItem = items[i];
    results.push({
        key: (fetchIndex + i).toString(),
        data: {
            title: dataItem.Title,
            thumbnail: dataItem.Thumbnail.Url,
            width: dataItem.Width,
            height: dataItem.Height,
            linkUrl: dataItem.Url,
            url: dataItem.MediaUrl
        }
    });
}
```
```

The return value, that's ultimately delivered through a promise, then has the `results` array as the item's data property, along with two other properties:

```
```javascript
return {
    items: results, // The array of items
    offset: requestIndex - fetchIndex, // The offset into the array for the requested item
    totalCount: that._maxCount,
};
```
```

The prefetching nature of the `item*` methods is helpful for the FlipView but essential for the ListView. This is demonstrated more clearly in the HTML ListView working with data sources sample that we saw earlier. Scenario 1 (see Figure 7-8) uses the same Bing Search data source as the FlipView sample with one small change. In the case of the FlipView, though, the page size is set between 1 and 10 and the largest number that the source will pull down at once is 100 items. In the ListView sample, the page size is set to 50 and the max number to 1000, as befits a collection control that will show more items at one time. Otherwise everything about the data source and the adapter is the same.