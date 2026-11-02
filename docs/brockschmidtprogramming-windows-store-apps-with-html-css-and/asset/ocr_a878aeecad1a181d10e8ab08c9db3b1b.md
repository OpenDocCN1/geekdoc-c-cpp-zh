Three flavors of download are supported in the WinRT API and reflected in the sample:

+   - A normal download at normal priority. Such a transfer continues to run when the app is suspended, but if it's a long transfer it could be slowed (throttled) or paused depending on system conditions like battery life and network type. The system supports up to five parallel transfers at normal priority.
+   - A normal download at high priority. Typically an app will set its most important download at a higher priority than others it starts at the same time. A high-priority transfer will start even if there are already five normal-priority downloads running. If you schedule multiple high-priority transfers, up to six of them will run in parallel (one plus replacing all of the five normal-priority downloads) until the high-priority queue is cleared, then normal-priority transfers are resumed.
+   - An *unconstrained* download at either priority. As noted before, an unconstrained download will continue to run (subject to user consent) even in modes like connected standby. You use this feature in scenarios where you know the user would want a transfer to continue possibly for a long period of time and not have it interrupted or paused.

Starting a download happens as follows. First create a StorageFile to receive the data (though this is not required, as we'll see later in this section). Then create a DownloadOperation object for the transfer using BackgroundDownloader.createDownload, to which you pass the URI of the data, the StorageFile in which to store it, and an optional StorageFile containing a request body to send to the server when starting the transfer (more on this later). In the operation object you can then set its priority, method, costPolicy, and transferGroup properties to override the defaults supplied by the BackgroundDownloader. The priority is a BackgroundTransferPriority value (default or high), and method is a string that identifies the type transfer being used (normally GET for HTTP or RETR for FTP). We'll come back to the other two properties later in the "Setting Cost Policy" and "Grouping Transfers" sections.

Once the operation is configured as needed, the last step is to call its startAsync method, which returns a promise to which you attach your completed, error, and progress handlers via then or done. Here's code from js/downloadFile.js.41

```
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
```
```

41 The code in the sample has more structure than shown here. It defines its own DownloadOperation class that unfortunately has the same name as the WinRT class, so I'm electing to omit mention of it.