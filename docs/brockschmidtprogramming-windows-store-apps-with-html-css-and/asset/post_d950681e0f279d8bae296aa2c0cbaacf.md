
The event args also contains a property called `neighboringFilesQuery`, which is a ready-made `StorageFileQueryResult` that allows you to retrieve sibling files even though they weren't actually selected or activated. This helps in creating gallery views for a folder that contains the activated file(s), and it's a good place to call the query's `findStartIndexAsync`, especially when using a semantic zoom control where you want to zoom to that index. In this case, the argument to `findStartIndexAsync` is one of the `StorageFile` objects within `eventArgs.detail.files` rather than a keyword.

**Caveat** With `neighboringFilesQuery`, the app still needs programmatic access to the folder in question, such as a library capabilities, otherwise you'll see access denied exceptions. Thus, the query is primarily useful for those libraries and not arbitrary folders.

Apps that declare the Removable Storage capability and at least one file type can also be launched with `ActivationKind.device`, which means the user selected to launch that app in response to an AutoPlay event when a device (like a camera) was attached to the system. An app will typically then do things like import images from that device. Scenario 4 of the [Removable storage sample](https://github.com/microsoft/Windows-universal-samples/tree/main/Samples/RemovableStorage) is activated for this launch kind, for example. The eventArgs here is WebUIDeviceActivatedEventArgs, the key property of which is eventArgs.detail.deviceInformationId that identifies the attached device. This sample passes that onto its page control in js/s4_autoplay.js (as arg) that then gets a virtual `StorageFolder` through `Windows.Devices.Portable.StorageDevice.FromId` and runs a file query to find images:

```javascript
var storage = (typeof arg === "string") ?
    Windows.Devices.Portable.StorageDevice.fromId(arg) : arg;
if (storage) {
    var storageName = storage.name;

    // Construct the query for image files
    var queryOptions = new Windows.Storage.Search.QueryOptions(
        Windows.Storage.CommonFileQuery.orderByName, [".jpg", ".png", ".gif"]);
    var imageFileQuery = storage.createFileQueryWithOptions(queryOptions);

    // Run the query for image files
    imageFileQuery.getFilesAsync().done(function (imageFiles) {
        // process results
    });
```
```

## What We've Just Learned

- User data lives anywhere outside the app's own app data folders (and package). User data locations span the local file system, removable storage devices, local networks, and the cloud, and the `StorageFile` and `StorageFolder` objects hide the details about how those locations are referenced and their access models.
- Access to user data folders, such as media libraries, documents, and removable storage, is controlled by manifest capabilities. Such capabilities need be declared only if the app needs to access the file system in some way other than using the file picker.
- The file picker is the way that users can select files from any safe location in the file system, as well as files that are provided by other apps (where those files might be remote, stored in a database, or otherwise not present as file entities on the local file system). The ability to select files directly from other apps—including files that another app might generate on demand—is one of the most convenient and powerful features of Windows Store apps.
- Apps should always use the `Windows.Storage.AccessCache` to preserve programmatic access to files and folders for later sessions. The cache maintains two independent lists: one for recently used items (limited to 25) and one for general purpose use (limited to 1000 items).
- SkyDrive is deeply integrated into Windows such that there is always at least a local placeholder file that will automatically download its contents (if allowed by the current network) when the file is open. The `StorageFile.isAvailable` flag indicates whether the file's contents are currently accessible.
- The `StorageFile` object provide access to rich metadata, including thumbnails and media specific properties.
- Apps should always use thumbnails to show image contents in consumption scenarios to avoid loading full image data. Loading the image is necessary only in editing and full-image panning views.
- The `StorageLibrary` object supplies the ability to manage which folders are included in the user's media libraries.
- `StorageFolder` objects provide a very rich and extensive capability to enumerate its contents and to query for items that match certain criteria. WinRT provides common file and folder queries for typical scenarios, but you can also build custom queries with Advanced Query Syntax (AQS) strings. Custom queries also provide prefetching capabilities for properties and thumbnails.
- The `WinJS.UI.StorageDataSource` object provides a built-in means with query support to create a gallery experience in a ListView control. A gallery should always use thumbnails for images and use the `isAvailable` flag to differentiate items in its UI.
- To support file activation, an app associates itself with one or more file types in its manifest and then watches for the `ActivationKind.File` whose event args will contain the `StorageFile` objects for the files that were launched, as well as a `neighboringFilesQuery` that provides access to other files in the folder.
- Apps that support removable storage can also associate themselves with one or more file types and be launched for Auto Play events with `ActivationKind.device`.

## Chapter 12

### Input and Sensors

Touch is clearly one of the most exciting means of interacting with a computer that has finally come of age. Sure, we've had touch-sensitive devices for many years: I remember working with a touch-enabled screen in my college days, which I have to admit is almost an embarrassingly long time ago now! In that case, the touch sensor was a series of transparent wires embedded in a plastic sheet over the screen, with an overall touch resolution of around 60 wide by 40 high...and, to really date myself, the monitor itself was only a text terminal!

Fortunately, touch screens have progressed tremendously in recent years. They are responsive enough for general purpose use (that is, you don't have to stab them to register a point), are built into high-resolution displays, are relatively inexpensive, and are capable of doing something more than replicating the mouse—namely, supporting multitouch and sophisticated gestures.

Great touch interaction is thus now a fundamental feature of great apps, and designing for touch means in many ways thinking through UI concerns anew. In your layout, for example, it means making hit targets a size that's suitable for a variety of fingers. In your content navigation, it means utilizing direct gestures such as swipes and pinches rather than relying on only item selection and navigation controls. Similarly, designing for touch means thinking through how gestures might enrich the user experience—and also how to provide for discoverability and user feedback that has generally relied on mouse-only events like hover.

All in all, approach your design as if touch was the only means of interaction that your users might have. At the same time, it's very important to remember that new methods of input seldom obsolete existing ones. Sure, punch cards did eventually disappear, but the introduction of the mouse did not obsolete keyboards. The availability of speech recognition or handwriting has not obsoleted neither mouse nor keyboard. I think the same is true for touch: it's really a complementary input method that has its own particular virtues but is unlikely to wholly supplant the others. As Bill Buxton of Microsoft Research has said, "Every modality, including touch, is best for something and worst for something else." I expect, in time, we'll see ourselves using keyboard, mouse, and touch together, just as we learned to integrate the mouse in what was once a keyboard-only reality.

Windows is designed to work well with all forms of input—to work great with touch, to work great with mice, to work great with keyboards, and, well, to just work great on diverse hardware! (And Windows Store certification requires this for apps as well.) For this reason, Windows provides a unified pointer-based input model wherein you can differentiate the different inputs if you really need to but can otherwise treat them equally. You can also focus more on higher-level gestures as well, which can arise from any input source, and not worry about raw pointer events at all. Indeed, the very fact that we haven't even brought this subject up until now, midway through this book, gives testimony to just how natural it is to work with all kinds of pointer input without having to think about it: the controls and
