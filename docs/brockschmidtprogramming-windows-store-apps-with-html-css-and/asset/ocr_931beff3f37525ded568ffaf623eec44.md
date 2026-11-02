Scenario 7 of the `File access sample` has additional demonstrations, letting you choose which list to work with. It shows that you can enumerate the `entries` collection of either list. As above, `entries` is an `AccessListEntryView` with a `size` property and `first`, `getAt`, `getMany`, and `indexOf` methods (basically a derivative of a vector view, which we saw in Chapter 6, "Data Binding, Templates, and Collections." This type is projected into JavaScript as an array, so you can also use the `[]` operator and methods like `forEach` as scenario 7 of the sample shows (js/scenario7.js):

```
```javascript
var mruEntries =
    Windows.Storage.AccessCache.StorageApplicationPermissions.mostRecentlyUsedList.entries;
if (mruEntries.size > 0) {
    var mruOutputText = "The MRU list contains the following item(s):<br />";
    mruEntries.forEach(function (entry) {
        mruOutputText += entry.metadata + "<br />";
    });
    outputDiv.innerHTML = mruOutputText;
}
```
```

Each entry in the `AccessListEntryView` is a simple `AccessListEntry` object that contains the item's `token` and a `metadata` property with the string you can include when adding an item to the list.

# ## StorageFile Properties and Metadata

In Chapter 10 (in the section "Folders, Files, and Streams") we began looking at the many methods and properties of the `StorageFile` object, limiting ourselves to the basics because many of its features apply primarily to user data files rather than those you'll create for your app state. Now we're ready to delve into all its details, a topic that will take us quite deep down a few rabbit holes!

> > **Note** Many of the properties and methods described here for `StorageFile` also apply to `StorageFolder` object, but for convenience we'll focus on `StorageFile`.

Let's just assume that you've obtained a `StorageFile` object of interest through some means, be it a file picker, a media library, a file activation, one of the static `StorageFile` methods like `getFileFromPathAsync` or `replaceWithStreamedFileAsync`, and so on. As we've seen in Chapter 10, you can open the file (obtaining a stream) through `openAsync`, `openReadAsync`, `openSequentialReadAsync`, and `openTransactedWriteAsync`. You can also manage the file on the file system (as you would through Windows Explorer) with `copyAsync`, `copyAndReplaceAsync`, `deleteAsync`, `moveAsync`, `moveAndReplaceAsync`, and `renameAsync`. And the purpose of many other properties and methods, listed below, should be quite apparent from their descriptions and we won't cover them more here. Refer to the `StorageFile` reference and the `File access sample` for all that.

| Property | Description |
| :--- | :--- |
| `name` | The simple filename string of the file, including the extension if appropriate. |
| `path` | The full pathname string of the file. |
| `displayName` | The file's name string as appropriate for UI, typically without the extension. |
| `fileType` | The file's extension string. `displayName` + `fileType` is the same as `name` at least on the local file system. |