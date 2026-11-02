
make sure you have the latest data. Note that you must use `HttpClient` rather than `WinJS.xhr` to exercise this degree of control.

## Background Transfer

A common use of HTTP requests is to transfer potentially large files to and from an online repository. For even moderately sized files, however, this presents a challenge: very few users typically want to stare at their screen to watch file transfer progress, so it's highly likely that they'll switch to another app to do something far more interesting while the transfer is taking place. In doing so, the app that's doing the transfer will be suspended and possibly even terminated. This does not bode well for trying to complete such operations using a mechanism like `HttpClient`!

One solution would be to provide a background task for this purpose, which was a common request with early reviews of Windows 8. However, there's little need to run app code for this common purpose, so WinRT provides a specific API, `Windows.Networking.BackgroundTransfer` (which includes the prefetcher, as we just saw at the end of the previous section). This API supports up to 500 scheduled transfers systemwide and typically runs five transfers in parallel. It offers built-in cost awareness and resiliency to changes in connectivity (switching seamlessly to the user's preferred network), relieving apps from such concerns. Transfers continue when an app is suspended and will be paused if the app is terminated (including if the user terminates the app with a gesture or Alt+F4), except for uploads (HTTP POST) which cannot be paused. When the app is resumed or launched again, it can then check the status of background transfers it previously initiated and take further action as necessary—processing downloaded information, notifying successful uploads in its UI (issuing toasts and tile updates is built into the API), and enumerating pending transfers, which will restart any that were paused or otherwise interrupted.

In short, use the background transfer API whenever you expect the operation to exceed your customer's tolerance for waiting. This clearly depends on the network's connection speed and whether you think the user will switch away from your app while such a transfer is taking place. For example, if you initiate a transfer operation but the user can continue to be productive (or entertained) in your app while that's happening, using HTTP requests directly might be a possibility, though you'll still be responsible for cost awareness and handling connectivity. If, on the other hand, the user cannot do anything more until the transfer is complete, you might choose to use background transfer for perhaps any data larger than 500K or some other amount based on the current network speed.

In any case, when you're ready to employ background transfer in your app, the `BackgroundDownloader` and `BackgroundUploader` objects will become your fast friends. Both objects have methods and properties through which you can enumerate pending transfers as well as perform general configuration of credentials, HTTP request headers, transfer method, cost policy (for metered networks), and grouping. Each individual operation is then represented by a `DownloadOperation` or `UploadOperation` object, through which you can control the operation (pause, cancel, etc.) and retrieve status. With each operation you can also set priority, credentials, cost policy, and so forth,

Three flavors of download are supported in the WinRT API and reflected in the sample:

- A normal download at normal priority. Such a transfer continues to run when the app is suspended, but if it's a long transfer it could be slowed (throttled) or paused depending on system conditions like battery life and network type. The system supports up to five parallel transfers at normal priority.
- A normal download at high priority. Typically an app will set its most important download at a higher priority than others it starts at the same time. A high-priority transfer will start even if there are already five normal-priority downloads running. If you schedule multiple high-priority transfers, up to six of them will run in parallel (one plus replacing all of the five normal-priority downloads) until the high-priority queue is cleared, then normal-priority transfers are resumed.
- An *unconstrained* download at either priority. As noted before, an unconstrained download will continue to run (subject to user consent) even in modes like connected standby. You use this feature in scenarios where you know the user would want a transfer to continue possibly for a long period of time and not have it interrupted or paused.

Starting a download happens as follows. First create a StorageFile to receive the data (though this is not required, as we'll see later in this section). Then create a DownloadOperation object for the transfer using BackgroundDownloader.createDownload, to which you pass the URI of the data, the StorageFile in which to store it, and an optional StorageFile containing a request body to send to the server when starting the transfer (more on this later). In the operation object you can then set its priority, method, costPolicy, and transferGroup properties to override the defaults supplied by the BackgroundDownloader. The priority is a BackgroundTransferPriority value (default or high), and method is a string that identifies the type transfer being used (normally GET for HTTP or RETR for FTP). We'll come back to the other two properties later in the "Setting Cost Policy" and "Grouping Transfers" sections.

Once the operation is configured as needed, the last step is to call its startAsync method, which returns a promise to which you attach your completed, error, and progress handlers via then or done. Here's code from js/downloadFile.js.41

```javascript
// Asynchronously create the file in the pictures folder (capability declaration required).
Windows.Storage.KnownFolders.picturesLibrary.createFileAsync(fileName,
    Windows.Storage.CreationCollisionOption.generateUniqueName)
    .done(function (newFile) {
        // Assume uriString is the text URI of the file to download
        var uri = Windows.Foundation.Uri(uriString);
        var downloader = new Windows.Networking.BackgroundTransfer.BackgroundDownloader();

        // Create a new download operation.
        var download = downloader.createDownload(uri, newFile);

        // Start the download
        var promise = download.startAsync().done(complete, error, progress);
    }
```

41 The code in the sample has more structure than shown here. It defines its own DownloadOperation class that unfortunately has the same name as the WinRT class, so I'm electing to omit mention of it.

While the operation is underway, the following properties provide additional information on the transfer:

- requestedUri and resultFile  The same as those passed to createDownload.
- guid  A unique identifier assigned to the operation.
- progress  A BackgroundDownloadProgress structure with bytesReceived, totalBytesToReceive, hasResponseChanged (a Boolean, see the getResponseInformation method below), hasRestarted (a Boolean set to true if the download had to be restarted), and status (a BackgroundTransferStatus value: idle, running, pausedByApplication, pausedCostedNetwork, pausedNoNetwork, canceled, error, and completed).

A few methods of DownloadOperation can also be used with the transfer:

- pause and resume  Control the download in progress. We'll talk more of these in the "Suspend, Resume, and Restart with Background Transfers" section below.
- getResponseInformation  Returns a ResponseInformation object with properties named headers (a collection of response headers from the server), actualUri, isResumable, and statusCode (from the server). Repeated calls to this method will return the same information until the hasResponseChanged property is set to true.
- getResultStreamAt  Returns an InputStream for the content downloaded so far or the whole of the data once the operation is complete.

In scenario 1 of the sample, the progress function—which is given to the promise returned by startAsync—uses getResponseInformation and getResultStreamAt to show a partially downloaded image:

```javascript
var currentProgress = download.progress;

// ...

// Get Content-Type response header.
var contentType = download.getResponseInformation().headers.lookup("Content-Type");

// Check the stream is an image.
if (contentType.indexOf("image/") === 0) {
    // Get the stream starting from byte 0.
    imageStream = download.getResultStreamAt(0);
}

// Convert the stream to a WinRT type
var msStream = MSApp.createStreamFromInputStream(contentType, imageStream);
var imageUrl = URL.createObjectURL(msStream);

// Pass the stream URL to the HTML image tag.
```
