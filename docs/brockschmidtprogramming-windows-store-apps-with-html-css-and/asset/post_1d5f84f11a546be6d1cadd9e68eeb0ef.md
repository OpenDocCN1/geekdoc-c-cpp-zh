
| VideoProperties | from StorageFile.properties.getVideoPropertiesAsync |  |
| Additional properties | System.Video, System.Media, System.Image, System.Photo |  |
| Property | DataType | Applicable Windows Property |
|---|---|---|
| title | String | System.Title |
| subtitle | String | System.Media.SubTitle |
| year | Number | System.Media.Year |
| publisher | String | System.Media.Publisher |
| rating | Number | System.Rating |
| width | Number in pixels | System.Video.FrameWidth |
| height | Number in pixels | System.Video.FrameHeight |
| orientation | A FileProperties.VideoOrientation object containing normal, rotate90, rotate180, rotate270 | System.Photo.Orientation |
| duration | Number (in 100ns units, i.e., 1/10th milliseconds) | System.Media.Duration |
| bitrate | Number (in bits/second) | System.Video.TotalBitrate, System.Video.EncodingBitrate |
| directors | String vector | System.Video.Director |
| producers | String vector | System.Media.Producer |
| writers | String vector | System.Media.Writer |
| keywords | String vector | System.Keywords |
| latitude | Double (see below) | System.GPS.LatitudeDecimal, or combination of System.GPS.Latitude, System.GPS.LatitudeDenominator, System.GPS.LatitudeNumerator, and System.GPS.LatitudeRef |
| longitude | Double (see below) | System.GPS.LongitudeDecimal, or combination of System.GPS.Longitude, System.GPS.LongitudeDenominator, System.GPS.LongitudeNumerator, and System.GPS.LongitudeRef |

| MusicProperties | from StorageFile.properties.getMusicPropertiesAsync |  |
| Additional properties | System.Music, System.Media |  |
| Property | DataType | Applicable Windows Property |
|---|---|---|
| title | String | System.Title, System.Music.AlbumTitle |
| subtitle | String | System.Media.SubTitle |
| trackNumber | Number | System.Music.TrackNumber |
| year | Number | System.Media.Year |
| publisher | String | System.Media.Publisher |
| artist | String | System.Music.Artist, System.Music.DisplayArtist |
| albumArtist | String | System.Music.DisplayArtist (read), System.Music.AlbumArtist (write) |
| genre | String vector | System.Music.Genre |
| composers | String vector | System.Music.Composer |
| conductors | String vector | System.Music.Conductor |
| rating | Number (1-99 with 0 meaning "no rating") | System.Rating |
| duration | Number (in 100ns units, i.e., 1/10th milliseconds) | System.Media.Duration |
| bitrate | Number (in bits/second) | System.Video.TotalBitrate, System.Video.EncodingBitrate |
| producers | String vector | System.Media.Producer |
| writers | String vector | System.Media.Writer |

| DocumentProperties | from StorageFile.properties.getDocumentPropertiesAsync |  |
| Additional properties | System |  |
| Property | DataType | Applicable Windows Property |
|---|---|---|
| title | String | System.Title |
| Author | String vector | System.Author |
| keywords | String vector | System.Keywords |
| Comments | String | System.Comment |

### Note
The `latitude` and `longitude` properties for images and video are double types but contain degrees, minutes, seconds, and a directional reference. The [Simple imaging sample] (in js\default.js) contains a helper function to extract the components of these values and convert them into a string:

```javascript
"convertLatLongToString": function (latlong, isLatitude) {
    var reference;

    if (isLatitude) {
        reference = (latlong >= 0) ? "N" : "S";
    } else {
        reference = (latlong >= 0) ? "E" : "W";
    }

    latlong = Math.abs(latlong);
    var degrees = Math.floor(latlong);
    var minutes = Math.floor((latlong - degrees) * 60);
    var seconds = ((latlong - degrees - minutes / 60) * 3600).toFixed(2);

    return degrees + "°" + minutes + "'" + seconds + "\"" + reference;
}
```

To summarize, the sign of the value indicates direction. A positive value for latitude means North, negative means South; for longitude, positive means East, negative means West. The whole number portion of the value provides the degrees, and the fractional part contains the number of minutes expressed in base 60. Multiplying this value by 60 gives the whole minutes, with the remainder then containing the seconds. Although this floating-point value isn't all that convenient for UI output, as we see here, it's what you typically want for coordinate math and talking with various web services.

Speaking of the Simple imaging sample, it's one of a few samples in the Windows SDK that demonstrate working with these properties. Scenario 1 (js\scenario1.js) provides the most complete demonstration because you can choose an image file and it will load and display various properties, as shown in Figure 11-12. I can verify that the date, camera make/model, and exposure information are all accurate.

![](img/0e8e4a2b6f953d3397e14e88cd5d8b4d_586_0.png)

### FIGURE 11-12
Image file properties in the Simple imaging sample, which is panned down to show the whole image and more of the property fields.

The sample's `openHandler` method is what retrieves these properties from the file using `StorageFile.properties.getImagePropertiesAsync` and `ImageProperties.retrievePropertiesAsync` for a couple of additional properties not already in `ImageProperties`. Then `getImagePropertiesForDisplay` coalesces these into a single object used by the sample's UI. Some lines are omitted in the code shown here:

```
    var ImageProperties = {};

    function openHandler() {
        // Keep data in-scope across multiple asynchronous methods.
        var file = {};

        Helpers.getFileFromOpenPickerAsync().then(function (_file) {
            file = _file;
            return file.properties.getImagePropertiesAsync();
        }).then(function (imageProps) {
            ImageProperties = imageProps;

            var requests = [
                "System.Photo.ExposureTime",       // In seconds
                "System.Photo.FNumber"             // F-stop values defined by EXIF spec
            ];

            return ImageProperties.retrievePropertiesAsync(requests);
        }).done(function (retrievedProps) {
            // Format the properties into text to display in the UI.
            displayImageUI(file, getImagePropertiesForDisplay(retrievedProps));
        });
    }
```

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
