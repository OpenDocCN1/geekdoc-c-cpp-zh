that's activated for this purpose receives those `StorageFile` objects in its activated handler and is automatically granted full programmatic access. This makes sense if you think about it: if the user activated the file(s) from Windows Explorer, they've implicitly given their consent in the process. And for another app to launch a file, it must first get to its `StorageFile` object, and that happens either through the file picker or some other means that has programmatic access.

Both sides of file activation are demonstrated in the Association launching sample. Let's start with scenarios 1 and 2 that show the launching part, as that's simple and straightforward.

To launch a given `StorageFile`, just call `Windows.System.Launcher.launchFileAsync`, the results of which is a Boolean indicating whether it was successful (js/launch-file.js):

```
~~~
// file is the StorageFile to launch
Windows.System.Launcher.launchFileAsync(file).done(
    function (success) {
        // success indicates whether the file was launched.
    });
~~~
```

**Note** The launcher blocks any file type that can contain executable code, such as exe, msi, js, etc.

Alternately, you can launch a URI by using the `launchUriAsync` method, which is typically used to launch a browser or an URI with a custom scheme (such as `mailto:`) that activates an app through protocol association. (We'll return to protocols in Chapter 15.) This is demonstrated in scenario 2 (js/launch-uri.js):

```
~~~
var uri = new Windows.Foundation.Uri(document.getElementById("uriToLaunch").value);

// Launch the URI.
Windows.System.Launcher.launchUriAsync(uri).done(
    function (success) {
        // success indicates whether the file was launched.
    });
~~~
```

**Note** `launchUriAsync` does not recognize `ms-appx`, `ms-appx-web`, or `ms-appdata` URIs, because these already map the current app. The app should just display such pages directly.

With both APIs you can control some aspects of the launching process by passing a `LauncherOptions` object as the second argument. Its properties are as follows:

| Property | Description |
| --- | --- |
| `contentType` | The content type associated with a URI (`launchUriAsync` only). |
| `desiredRemainingView` | A value from `Windows.UI.ViewManagement.ViewSizePreference` (see Chapter 8), indicating how the calling app should appear after the launch (default, useLess, useHalf, useMore, useMinimum, or useNone). This helps when implementing cross-app scenarios, although the choice is not guaranteed. |