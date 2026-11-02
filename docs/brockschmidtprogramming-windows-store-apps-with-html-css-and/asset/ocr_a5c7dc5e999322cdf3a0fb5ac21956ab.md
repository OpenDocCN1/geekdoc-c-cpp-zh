To that group of properties you can also specify a custom list in the second argument, with each property name in quotes, such as ["System.CopyRight", "System.Image.ColorSpace"]; for no custom properties, just pass []. Remember that you can also use strings from the [SystemProperties](#) object in [Windows.Storage](#).

This, in fact, is exactly what you see in an example of the API, found in scenario 3 of the [Folder enumeration sample](#) that we’ve been looking at already (js/scenario3.js):

```
var search = Windows.Storage.Search;
var fileProperties = Windows.Storage.FileProperties;

// Create query options with common query sort order and file type filter.
var fileTypeFilter = [".jpg", ".png", ".bmp", ".gif"];
var queryOptions = new Search.QueryOptions(search.CommonFileQuery.OrderByName, fileTypeFilter);

// Set up property prefetch - use the PropertyPrefetchOptions for top-level properties
// and an array for additional properties.
var imageProperties = fileProperties.PropertyPrefetchOptions.ImageProperties;
var copyrightProperty = "System.CopyRight";
var colorSpaceProperty = "System.Image.ColorSpace";
var additionalProperties = [copyrightProperty, colorSpaceProperty];
queryOptions.SetPropertyPrefetch(imageProperties, additionalProperties);

// Query the Pictures library.
var query = Windows.Storage.KnownFolders.PicturesLibrary
    .CreateFileQueryWithOptions(queryOptions);
```

[setThumbnailPrefetch](#) is similar, where you specify a ThumbnailMode, a requested size, and options, all of which are the same as discussed in the “Thumbnails” section earlier. The same scenario of the Folder enumeration sample shows a use of this, before the call to [createFileQueryWithOptions](#) (js/scenario3.js):

```
var thumbnailMode = fileProperties.ThumbnailMode.picturesView;
var requestedSize = 190;
var thumbnailOptions = fileProperties.ThumbnailOptions.UseCurrentScale;
queryOptions.SetThumbnailPrefetch(thumbnailMode, requestedSize, thumbnailOptions);
```

Clearly, you’d often use a thumbnail prefetch when creating a gallery experience with a ListView control, where you’d typically be using a [WinJS.UI.StorageDataSource](#) object as well. In fact, the [StorageDataSource](#) has its own options that it uses to automatically set up the appropriate prefetching, in which case you don’t use the [QueryOptions](#) directly. We’ll see this in the next section.

# Creating Gallery Experiences

In Chapter 7 we learned about the three components of a collection control: a data source, a layout, and templates. One of the most common uses of a collection control—especially the ListView—is to display a gallery of entities in the file system, organized in interesting ways. This section brings together much of what we’ve learned in this chapter where implementing such an experience is concerned: