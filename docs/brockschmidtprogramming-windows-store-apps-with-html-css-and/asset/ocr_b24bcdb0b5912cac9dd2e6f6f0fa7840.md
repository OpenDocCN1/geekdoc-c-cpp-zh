You can test all this by running the HereMyAm3b app, taking a suitable picture and making sure you have a location. Then use the Suspend and Shutdown option on the Visual Studio toolbar to terminate the app. Set a breakpoint on the updatePosition call above, and then restart the app in the debugger. You'll see that sessionState.lastPosition is initialized at that point.

With the last captured picture, we don't need to save the StorageFile, just the URI: we copied the file into our local appdata (so it persists across sessions already) and can just use the ms-appdata:// URI scheme to refer to it. When we capture an image, we just save that URI into sessionState.imageURI (the property name is arbitrary) at the end of the promise chain inside capturePhoto:

```
app.sessionState.imageURI = "ms-appdata:////local/HereMyAm/" + newFile.name;
```

Again, because imageURI is saved within sessionState, this value will be available when the app is restarted after being terminated. We also need to re-initialize lastCapture with a StorageFile so that the image is available through the Share contract. For this we can use Windows.Storage.StorageFile.getFileFromApplicationUriAsync. Here, then, is the code within the previousExecutionState == terminated case during activation:

```
//WinJS reloads the sessionState object here: initialize from the saved image URI and location.
if (app.sessionState.imageURI) {
  var uri = new Windows.Foundation.Uri(app.sessionState.imageURI);
  Windows.Storage.StorageFile.getFileFromApplicationUriAsync(uri).done(function (file) {
    lastCapture = file;
    var img = document.getElementById("photoImg");
    scaleImageToFit(img, document.getElementById("photo"), file);
  });
}

updatePosition();
```

As always, the code to set img.src with a thumbnail happens inside scaleImageToFit. This call is also inside the completed handler here because we want the image to appear only if we can also access its StorageFile again for sharing. Otherwise the two features of the app would be out of sync.

In all of this, note again that we don't need to explicitly reload these variables within the terminated case because WinJS reloads sessionState automatically. If we managed our state more directly, such as storing some variables in roaming settings within the checkpoint event, we would reload and apply those values at this time.

Note Using ms-appdata:/// and getFileFromApplicationUriAsync (or its sibling getFileFromPathAsync) works because the file exists in a location that we can access programmatically by default. It also works for libraries for which we declare a capability in the manifest. If, however, we obtain a StorageFile from the file picker, we need to save that in the Windows.Storage.AccessCache to preserve access permissions across sessions. We'll revisit the access cache in Chapter 11, "The Story of State, Part 2."