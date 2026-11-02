a QueryOptions from scratch, setting up its own sorting by System.IsFolder and System.ItemName. Other options we give to the StorageDataSource set up thumbnails, which are used to call the QueryOption.setThumbnailPrefetch method on our behalf. The result is a data source over a query that should perform well by default (js/scenario2ListView.js; code slightly edited):

```
function loadListViewControl() {
    // Build datasource from the pictures library
    var library = Windows.Storage.KnownFolders.picturesLibrary;
    var queryOptions = new Windows.Storage.Search.QueryOptions;

    // Shallow query to get the file hierarchy
    queryOptions.folderDepth = Windows.Storage.Search.FolderDepth.shallow;

    // Order items by type so folders come first
    queryOptions.sortOrder.clear();
    queryOptions.sortOrder.append({ascendingOrder: false, propertyName: "System.IsFolder"});
    queryOptions.sortOrder.append({ascendingOrder: true, propertyName: "System.ItemName"});
    queryOptions.indexerOption =
        Windows.Storage.Search.IndexerOption.useIndexerWhenAvailable;

    var fileQuery = library.createItemQueryWithOptions(queryOptions);
    var dataSourceOptions = {
        mode: Windows.Storage.FileProperties.ThumbnailMode.picturesView,
        requestedThumbnailSize: 190,
        thumbnailOptions: Windows.Storage.FileProperties.ThumbnailOptions.none
    };

    var dataSource = new WinJS.UI.StorageDataSource(fileQuery, dataSourceOptions);

    // Create the ListView using dataSource...
};
```

Within its storageRenderer function (the item renderer), the sample uses the StorageDataSource.loadThumbnail method to load up the prefetched thumbnails and display them in their img elements.

If you're interested, you can dig into the WinJS sources (the ui.js file) and see how StorageDataSource works with its queries and sets up an observable collection. Along the way, you'll run into one more set of WinRT APIs: Windows.Storage.BulkAccess. This was originally created for the StorageDataSource but is now considered deprecated. If you create your own data source or collection control, just use the enumeration and prefetch APIs we've already discussed.

# File Activation and Association

As noted a number of times already, an app typically obtains StorageFile and StorageFolder objects either from locations where it already has programmatic access or through the picker APIs. But there is a third option: when an app is associated with a particular file type, the user and/or other apps can launch a file or files, which in turn launches an associated app to handle them. In the process, the app