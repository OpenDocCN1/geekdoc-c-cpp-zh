WinRT collection class that you can instantiate directly, as we must do here.

+   - The Helpers.convertStarsToSystemRating method (also in js/default.js) converts between 1–5 stars, as used in the WinJS.UI.Rating control, to the System.Rating value that uses a 1–99 range. The documentation for System.Rating specifically indicates this mapping.

In general, all the detailed information you want for any particular Windows property can be found on the reference page for that property. Again start at Windows Properties and drill down from there.

# Folders and Folder Queries

Now that we've seen everything we can do with a StorageFile and file properties, it's time to turn our attention to the folders and libraries in which those files live and the StorageFolder and StorageLibrary objects that represent them.

As with StorageFile, we've already peeked at some of the basic StorageFolder methods in Chapter 10, such as createFileAsync, createFolderAsync, getFileAsync, getFolderAsync, getItemAsync, getFolderFromPathAsync, deleteAsync, and renameAsync. It also has many of the same properties as a file, including name, path, displayName, displayType, attributes, folderRelativeId, dateCreated, provider, and properties. It also shares a number of identical methods: isEqual, isOfType, getThumbnailAsync, getScaledImageAsThumbnailAsync, and getBasicPropertiesAsync. Everything about these is the same as for files, so please refer back to the "StorageFile Properties and Metadata" section for the details.

Be mindful, though, that the Windows properties you can retrieve and modify on a folder differ from those supported by files. For example, you can use StorageFolder.properties.retrievePropertiesAsync for the System.FreeSpace property and you'll actually get the free space on the drive where the folder lives. Pretty cool, eh?

Then there are the unique aspects of StorageFolder:

+   - tryGetItemAsync Identical to getItemAsync (to retrieve a contained item) except that it results in null (to your completed handler) for the most common errors instead of calling your error handler. This can simplify app logic. getItemAsync, on the other hand, will succeed if the item exists invokes your error handler for all error cases. For a simple demonstration, see scenario 11 of the File access sample.
+   - getFilesAsync, getFoldersAsync, and getItemsAsync These are the basic methods to enumerate the immediate contents of a folder depending on whether you want files only, folders only, or both, respectively. Each method results in a vector of the appropriate object type—StorageFile, StorageFolder, or StorageItem—as discussed in the "Simple Enumeration and Common Queries" section below.