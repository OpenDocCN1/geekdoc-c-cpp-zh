
Assuming the query is supported and succeeds when run, the result is just a flat list of files (a `StorageFile` vector) that you can easily iterate.

Folder queries are a little more complicated because the `StorageFolderQueryResult.getFoldersAsync` method gives you a `StorageFolder` vector, where each one is a *virtual folder* that's used to group files according to the query. That is, each folder does not represent an actual folder on whatever location was queried but is simply used to organize the results and help you present them in your UI. The `displayName` and other properties of each `StorageFolder` can be used to create group headings, and the files within each folder that you enumerate with `StorageFolder.getFilesAsync` are that group's contents.

Scenario 2 of the Folder enumeration sample demonstrates this with `groupByMonth`, `groupByTag`, and `groupByRating` queries on the pictures library. It runs each query like so, using the same processing code for the results (js/scenario2.js; I've shortened one variable name for brevity):

```javascript
var pix = Windows.Storage.KnownFolders.picturesLibrary;
var query = pix.createFolderQuery(Windows.Storage.Search.CommonFolderQuery.groupByTag);
query.getFoldersAsync().done(outputFoldersAndFiles);
```

The query variable, to be clear, is the `StorageFolderQueryResult` object, and calling its `getFoldersAsync` is what performs the actual enumeration. The `outputFoldersAndFiles` function—which is a completed handler—receives and iterates the resulting `StorageFolder` vectors, calling `getFilesAsync` for each and joining the resulting promises. It then processes each folder's results when they're all ready to show the output (js/scenario2.js):

```javascript
function outputFoldersAndFiles(folders) {
    // Add all file retrieval promises to an array of promises
    var promises = folders.map(function (folder) {
        return folder.getFilesAsync();
    });
    // Aggregate the results of multiple asynchronous operations
    // so that they are returned after all are completed. This
    // ensures that all groups are displayed in order.
    WinJS.Promise.join(promises).done(function (folderContents) {
        for (var i in folderContents) {
            // Create a group for each of the file groups
            var group = outputResultGroup(folders.getAt(i).name);
            // Add the group items in the group
            outputItems(group, folderContents[i]);
        }
    });
}
```

This is a marvelously concise piece of code, so let me explain what's happening. First, `folders` is the `StorageFolder` vector, and because we can treat it as an array we can use `folders.map` to execute a function for each folder in the vector. The `promises` variable is then an array of promises, one for each folder's `getFilesAsync`. Passing this to `WinJS.Promise.join`, if you remember from Chapter 3, "App Anatomy and Performance Fundamentals," returns a promise that is fulfilled when all the promises in the array are fulfilled, so this effectively waits for each one to complete.

The completed handler for `join` then receives an array that contains all the results of the individual promises. This handler then simply iterates that array, calling the sample's `outputResultGroup` and `outputItems` methods for each set, which just build up a DOM tree for the display. The results for my pictures library with `groupByTag` are as follows (revealing a small extent of my travels!):

A-Picture Tags/Places/Overseas/Egypt (3)
2008-02-29_009.JPG
2008-02-29_020.JPG
2008-02-29_035.JPG
A-Picture Tags/Places/Overseas/India (3)
159-16 Taj Mahal, Agra, India 9-98.JPG
159-37 Taj Mahal, Agra, India 9-98.JPG
160-7 Taj Mahal, Agra, India 9-98.JPG
A-Picture Tags/Places/States/Oregon/Outdoors/Oregon Coast (1)
122-10 Sunset, Pacific Beach, WA 6-95.JPG
A-Picture Tags/Places/States/Southwest/Arizona (3)
84-13 Sunset Crater and Tree, AZ 5-93.JPG
85-7 Ruins at Sunset, Wupatki NM, AZ 5-93.JPG
85-12 Wupatki Ruins Sunset, AZ 5-93 (2).jpg
A-Picture Tags/Places/States/Southwest/Colorado (1)
237-26 Flower Close-Ups, Rocky Mountain NP, CO 6-06.JPG
A-Picture Tags/Places/Family/Ocean Shores (28)
226-5 Seagulls in Sunset, Ocean Shores, WA 9-03.JPG
226-34 Sunset, Ocean Shores, WA 9-03.JPG
227-11 Sunset, Ocean Shores, WA 9-03.JPG

As for scenario 3 of the sample, that brings us into the matter of query options, which are discussed in the next section.

## Custom Queries

Now that we've seen the basics of enumerating folder contents with common queries and processing their results, we're ready to look at the full query capabilities offered by WinRT wherein you construct a custom query from scratch using a `QueryOptions` object. (The common queries are just shortcuts for typical cases to save you the trouble.) A custom query basically gives you all the capabilities that you have through the search features of the desktop Windows Explorer, using whatever Windows Properties you require.

As with the common queries, not all locations support custom queries, so once you've built the `QueryOptions` you want to call `StorageFolder.areQueryOptionsSupported` with that object. If it returns `true`, you can proceed. If you attempt to query a folder with unsupported options, expect a "parameter is incorrect" exception.

Something else you might want to know ahead of time is whether the folder itself has been indexed, which greatly affects the potential speed of the query. You do this through `StorageFolder.getIndexedStateAsync`. This results in an `IndexedState` value: `notIndexed`, `partiallyIndexed`, `fullyIndexed`, and `unknown`. Do note a fully indexed folder could yet contain nonindexed folders, but
generally speaking an indexed folder will produce results more quickly than the others.

The next step is to create the query by passing your query options to one of the three `StorageFolder` methods that accept them: `createFileQueryWithOptions`, `createFolderQueryWithOptions`, and `createItemQueryWithOptions`. These result in `StorageFileQueryResult`, `StorageFolderQueryResult`, and `StorageItemQueryResult` objects, as already discussed in the previous section. With these you can enumerate the results however you need, just as you do when you use a common query.

If you remember from earlier, the `getCurrentQueryOptions` and `applyNewQueryOptions` methods of `Storage[File | Folder | Item]QueryResult` work with the `QueryOptions` that were used to create the query. The `get` method retrieves the `QueryOptions` object, obviously, and calling the `apply` method will change the query mid-flight, firing the query result's `optionsChanged` event.

Ultimately, these queries involve what are known as Advanced Query Syntax (AQS) strings that are capable of identifying and describing as many specific criteria you desire. Each criteria is a Windows Property (again see *Windows properties* for the reference) such as `System.ItemDate`, `System.Author`, `System.Keywords`, `System.Photo.LightSource`, and so on.85 Each property can contain a target value such as `System.Author(Patrick OR Bob)` and `System.ItemType: "mp3"`, and terms can be combined with AND (which is implicit), OR, and NOT operators, in `System.Keywords: "needs review" AND (System.ItemType: "doc" OR System.ItemType: "docx")`.

> **Tip** The AND, OR, and NOT operators must be in uppercase or else they are interpreted as a keyword. Also note that quotation marks aren't strictly necessary.

Simply said, an AQS string is exactly what you can type into the search control of Windows Explorer. You can also try out AQS strings through the `Programmatic file search sample`, which we'll see in a moment once we look at the `QueryOptions` object that is so central to this process (it's where you provide AQS strings).

First, there are three `QueryOptions` constructors:

- `new QueryOptions()` Creates an uninitialized object.
- `new QueryOptions(<CommonFolderQuery>)` Creates an object pre-initialized from a `CommonFolderQuery`.
- `new QueryOptions(<CommonFileQuery>, <file_types>)` Creates an object pre-initialized from a `CommonFileQuery` along with an array of file types—for example, `["*.jpg", "*.jpeg", "*.png"]`. If you specify `null` for `<file_types>`, it's the same as `["*"]`.

85. Contrary to any examples in the documentation, queries should always use the full name of Windows properties such as `System.ItemDate`; rather than the user-friendly shorthand `date`: because the latter will not work on localized builds of Windows.
