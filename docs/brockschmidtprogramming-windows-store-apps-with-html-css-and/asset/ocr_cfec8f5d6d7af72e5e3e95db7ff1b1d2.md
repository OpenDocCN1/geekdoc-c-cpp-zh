Programmatically, you can refer to these locations in several ways. First, you can use the `ms-appdata:///` URI scheme as we saw in Chapter 3, where `ms-appdata:///local`, `ms-appdata:///roaming`, and `ms-appdata:///temp` refer to the individual folders and their contents. (Note the triple slashes: it's a shorthand allowing you to omit the package name.) You can also use the object returned from the `Windows.Storage.ApplicationData.current` method, which contains all the APIs you need to work with state, as we'll see.

By the way, you might have some read-only state directly in file in your app package. You can reference these with URIs that just start with / (meaning `ms-appx:///`). You can also get to them through the `StorageFolder` object from the `Windows.ApplicationModel.Package.current.installedLocation` property. We'll come back to the `StorageFolder` class a little later.

# ## App Data APIs (WinRT and WinJS)

We've answered the questions of “What kinds of state do we need to concern ourselves with?” and “Where does state live?” Now we can answer the third question, “What affects and modifies that state?”—a subject that will occupy the next 25 pages!

Much of the answer begins with the `ApplicationData` object that you get from the `Windows.Storage.ApplicationData.current` property, which is completely configured for your particular app. This object contains the following, where other object types are also found in the `Windows.Storage` namespace:

+   - `localFolder`, `temporaryFolder`, and `roamingFolder` Each of these properties is a `StorageFolder` object that allows you to create whatever files and additional folder structures you want in these locations (but note the `roamingStorageQuota` below).

+   - `localSettings` and `roamingSettings` These properties are `ApplicationDataContainer` objects that provide for managing a hierarchy of key-value settings pairs or composite groups of such pairs. All these are stored in the `AppData\Settings` folder in the `settings.dat` file.

+   - `roamingStorageQuota` This property contains the number of kilobytes that Windows will automatically roam for the app (typically 100); if the total data stored in `roamingFolder` and `roamingSettings` exceeds this amount, roaming will be suspended until the amount falls below the quota. You have to track how much data you store yourself if you think you might risk exceeding the quota.

+   - `dataChanged` An event indicating the contents of the `roamingFolder` or `roamingSettings` have been synchronized from the cloud, in which case an app should re-read its roaming state. It also indicates that some other part of the app (running code or a background task) has called the `signalDataChanged` method. (Note: `dataChanged` is a WinRT event for which you need to use `removeEventListener` as described in Chapter 3 in the “WinRT Events and removeEventListener” section.)