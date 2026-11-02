```
return local.createFolderAsync("HereMyAm",
    Windows.Storage.CreationCollisionOption.openIfExists);

//Note: the results from the returned promise are fed into the
//completed handler given to the next then in the chain.
})
.then(function (myFolder) {
    //Again, check validity of the result
    if (!myFolder) { throw ('could not create local appdata folder'); }

    //Append file creation time to the filename (should avoid collisions,
    //but need to convert colons)
    var newName = "Capture - " +
        capturedFile.dateCreated.toString().replace(/:/g, "-") + capturedFile.fileType;

    //Make the copy
    return capturedFile.copyAsync(myFolder, newName);
})
.then(function (newFile) {
    if (!newFile) { throw ('could not copy file'); }

    lastCapture = newFile; //Save for Share
    img.src = "ms-appdata:///local/HereMyAm/" + newFile.name;
    //newFile.name includes extension

    scaleImageToFit(img, photoDiv, newFile);

    //Delete the temporary file
    return capturedFile.deleteAsync();
})
//No completed handler needed for the last operation
.done(null, function (error) {
    console.log("Unable to invoke capture UI:" + error.message);
});
```

This might look a little complicated to you at this point, but trust me, you'll quickly become accustomed to this structure when dealing with multiple async operations. If you can look past all the syntactical ceremony here and simply follow the words Async and then, you can see that the sequence of operations is simply this:

+   - Capture an image from the camera capture UI, resulting in a temp file, then...
+   - Create or open the HereMyAm folder in local appdata, resulting in a folder object, then...
+   - Copy the captured file to that folder, resulting in a new file, then...
+   - Delete the temp file, which has no results, and we're done.

To help you follow the chain, I've use different colors in the code above to highlight each set of async calls and their associated then methods and results, along with a final call to done. What works very well about this chaining structure—which is much cleaner than trying to nest operations within each completed handler—is that any exceptions that occur, whether from WinRT or a direct throw, are