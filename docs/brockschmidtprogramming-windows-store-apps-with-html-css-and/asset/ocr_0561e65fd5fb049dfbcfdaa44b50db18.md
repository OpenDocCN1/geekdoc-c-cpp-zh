+   - The file picker is the way that users can select files from any safe location in the file system, as well as files that are provided by other apps (where those files might be remote, stored in a database, or otherwise not present as file entities on the local file system). The ability to select files directly from other apps—including files that another app might generate on demand—is one of the most convenient and powerful features of Windows Store apps.
+   
+   - Apps should always use the `Windows.Storage.AccessCache` to preserve programmatic access to files and folders for later sessions. The cache maintains two independent lists: one for recently used items (limited to 25) and one for general purpose use (limited to 1000 items).
+   
+   - SkyDrive is deeply integrated into Windows such that there is always at least a local placeholder file that will automatically download its contents (if allowed by the current network) when the file is open. The `StorageFile.isAvailable` flag indicates whether the file's contents are currently accessible.
+   
+   - The `StorageFile` object provide access to rich metadata, including thumbnails and media specific properties.
+   
+   - Apps should always use thumbnails to show image contents in consumption scenarios to avoid loading full image data. Loading the image is necessary only in editing and full-image panning views.
+   
+   - The `StorageLibrary` object supplies the ability to manage which folders are included in the user's media libraries.
+   
+   - `StorageFolder` objects provide a very rich and extensive capability to enumerate its contents and to query for items that match certain criteria. WinRT provides common file and folder queries for typical scenarios, but you can also build custom queries with Advanced Query Syntax (AQS) strings. Custom queries also provide prefetching capabilities for properties and thumbnails.
+   
+   - The `WinJS.UI.StorageDataSource` object provides a built-in means with query support to create a gallery experience in a ListView control. A gallery should always use thumbnails for images and use the `isAvailable` flag to differentiate items in its UI.
+   
+   - To support file activation, an app associates itself with one or more file types in its manifest and then watches for the `ActivationKind.File` whose event args will contain the `StorageFile` objects for the files that were launched, as well as a `neighboringFilesQuery` that provides access to other files in the folder.
+   
+   - Apps that support removable storage can also associate themselves with one or more file types and be launched for Auto Play events with `ActivationKind.device`.