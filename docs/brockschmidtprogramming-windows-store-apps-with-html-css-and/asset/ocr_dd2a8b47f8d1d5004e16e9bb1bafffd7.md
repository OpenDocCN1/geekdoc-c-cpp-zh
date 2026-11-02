```
function getImagePropertiesForDisplay(retrievedProps) {
    // If the specified property doesn't exist, its value will be null.
    var orientationText = Helpers.getOrientationString(ImageProperties.orientation);

    var exposureText = retrievedProps.lookup("System.Photo.ExposureTime") ?
        retrievedProps.lookup("System.Photo.ExposureTime") * 1000 + " ms" : "";

    var fNumberText = retrievedProps.lookup("System.Photo.FNumber") ?
        retrievedProps.lookup("System.Photo.FNumber").toFixed(1) : "";

    // Omitted: Code to convert ImageProperties.latitude and ImageProperties.longitude to
    // degrees, minutes, seconds, and direction

    return {
        "title": ImageProperties.title,
        "keywords": ImageProperties.keywords, // array of strings
        "rating": ImageProperties.rating, // number
        "dateTaken": ImageProperties.dateTaken,
        "make": ImageProperties.cameraManufacturer,
        "model": ImageProperties.cameraModel,
        "orientation": orientationText,
        // Omitted: lat/long properties
        "exposure": exposureText,
        "fNumber": fNumberText
    };
}
```

Most of the displayImageUI function to which these properties are passed just copies the data into various controls. It's good to note again, though, that displaying the picture itself is easily accomplished with our good friend, URL.createObjectURL, but as we learned earlier in this chapter, it would be better to avoid loading the whole image file and instead use a thumbnail from StorageFile.getScaledImageThumbnailAsync. That is, change this line of code in displayImage.js (js/scenario1.js):

```
id('outputImage').src = window.URL.createObjectURL(file, { oneTimeOnly: true });
```

to the following:

```
var mode = Windows.Storage.FileProperties.ThumbnailMode.singleItem;
file.getScaledImageThumbnailAsync(mode, 500).done(function (thumb) {
    var img = id('outputImage');
    img.src = URL.createObjectURL(thumb, { oneTimeOnly: true });
    img.onload = function () {
        thumb.close();
    }
});
```

A bit more code to write, but definitely more efficient!

For MusicProperties a small example can be found in the Playlist sample and another in the Configure keys for media sample, both of which we'll see in Chapter 13. The latter especially shows how to use the music properties to obtain album art. As for VideoProperties and DocumentProperties, the SDK doesn't have samples for these, but working with them follows the same pattern as shown