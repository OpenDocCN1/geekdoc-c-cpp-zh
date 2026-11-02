```
```
// [More output code omitted to highlight System.FileName occurrences]
};
});
```
```

To keep things simple, I just ran a search on "Horses" that results in just the one file, "~ 08 - Horses, Sleeping.mp3". The map that I got back in the `searchHits` variable contained the following (only one location per property):

| Property | startPosition | Length |
|---|---|---|
| System.FileName | 7 | 6 |
| System.ItemNameDisplay | 7 | 6 |
| System.ItemPathDisplay | 65 | 6 |
| System.ParsingName | 7 | 6 |
| System.Title | 0 | 6 |

Clearly, you can see that position 7 (zero-based) in the filename is where "Horses" begins. The `System.Title` of the track is just "Horses, Sleeping," so its start position is appropriately 0.

In some cases, as with my "Nightingale" search before, the term might not occur in the filename or title at all. In such cases you'll see a completely different list of properties in the map, such as `System.ItemFolderNameDisplay` and `System.MusicAlbumTitle`.

# ## Metadata Prefetching with Queries

The `QueryOptions.setPropertyPrefetch` method allows you to indicate a group of file properties that you want to optimize for fast retrieval—they're accessed through the same APIs as properties are otherwise, but they come back faster. This is very helpful when you're displaying a collection of files in a ListView, using a custom data source with certain properties from enumerated files. In that case, you'd want to set those up for prefetch so that the control renders faster. Similarly, the `setThumbnailPrefetch` method tells Windows what kinds of thumbnails you want to include in the query—again, you can ask for these without setting the prefetch, but they come back faster when you do. This helps you optimize the display of a file collection.

Examples of this can be found in two samples. In scenario 3 of the Semantic text query sample, which we saw at the end of the previous section, it made sure to prefetch the music properties it planned to search (`js\filePropertiesMatches.js`):

```
```
options.setPropertyPrefetch(
    Windows.Storage.FileProperties.PropertyPrefetchOptions.musicProperties, []);
```
```

The values are affected by the first argument to `setPropertyPrefetch`, which comes from `PropertyPrefetchOptions`: none, musicProperties, videoProperties, imageProperties, documentProperties, and basicProperties. If something sounds familiar here, it's because these exactly match the objects returned through methods of the `StorageFile.properties` object, such as `retrieveMusicPropertiesAsync`, as discussed in "Media-Specific Properties" earlier.