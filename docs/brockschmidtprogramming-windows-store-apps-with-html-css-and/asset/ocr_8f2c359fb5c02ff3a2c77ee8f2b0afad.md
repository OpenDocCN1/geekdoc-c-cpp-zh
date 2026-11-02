For this event, the handler receives a Windows.ApplicationModel.DataTransfer.DataRequest object in the event args (e.request), which in turn holds a DataPackage object (e.request.data). To make data available for sharing, you populate this data package with the various formats you have available, as we've saved in lastPosition and lastCapture. So in our case, we make sure we have position and a photo and then fill in text and image properties (if you want to obtain a map from Bing for sharing purposes, see Get a static map):

```
//Drop this in after capturePhoto
function provideData(e) {
  var request = e.request;
  var data = request.data;

  if (!lastPosition || !lastCapture) {
    //Nothing to share, so exit
    return;
  }

  data.properties.title = "Here My Am!";
  data.properties.description = "At (" 
    + lastPosition.latitude + ", " + lastPosition.longitude + ")";

  //When sharing an image, include a thumbnail
  var streamReference = 
    Windows.Storage.Streams.RandomAccessStreamReference.createFromFile(lastCapture);
  data.properties.thumbnail = streamReference;

  //It's recommended to always use both setBitmap and setStorageItems for
  // sharing a single image since the target app may only support one or the other.

  //Put the image file in an array and pass it to setStorageItems
  data.setStorageItems([lastCapture]);

  //The setBitmap method requires a RandomAccessStream.
  data.setBitmap(streamReference);
}
```

The latter part of this code is pretty standard stuff for sharing a file-based image (which we have in lastCapture). I got most of this code, in fact, directly from the Share content source app sample, which we'll look at more closely in Chapter 15, "Contracts." We'll also talk more about files and streams in Chapter 10.

With this last addition of code, and a suitable sharing target installed (such as the Share content target app sample, as shown in Figure 2-20, or Twitter as shown in Figure 2-21, we now have a very functional app—in all of 35 lines of HTML, 125 lines of CSS, and less than 100 lines of JavaScript!