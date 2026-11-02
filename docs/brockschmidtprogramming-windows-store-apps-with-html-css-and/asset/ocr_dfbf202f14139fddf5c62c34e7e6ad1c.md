content. In js\scenario3.js we save credential within the completed handler for
CredentialPicker.pickAsync:

```
```javascript
//results.credential will be null if the user cancels
if (results.credential != null) {
    //Having retrieved a credential, write the opaque buffer to a file
    var option = Windows.Storage.CreationCollisionOption.replaceExisting;

    Windows.Storage.ApplicationData.current.localFolder.createFileAsync("credbuffer.dat",
        option).then(function (file) {
            return Windows.Storage.FileIO.writeBufferAsync(file, results.credential);
        }).done(function () {
            //No results for this operation
            console.log("credbuffer.dat written.");
        }, function (e) {
            console.log("Could not create credbuffer.dat file.");
        });
}
```
```

I’m using the local appdata folder here; you could also use the roaming folder if you want the
credential to roam (securely) to other devices as if it were saved in the Credential Locker.

To reload, we modify the launchCredPicker function to accept a buffer and use that for
previousCredential if given:

```
```javascript
function launchCredPicker(prevCredBuffer) {
    try {
        var options = new Windows.Security.Credentials.UI.CredentialPickerOptions();

        //Set the previous credential if provided
        if (prevCredBuffer != null) {
            options.previousCredential = prevCredBuffer;
        }
```
```

We then point the click handler for button1 to a new function that looks for and loads the
credbuffer.dat file and calls launchCredPicker accordingly:

```
```javascript
function readPrevCredentialAndLaunch() {
    Windows.Storage.ApplicationData.current.localFolder.getFileAsync("credbuffer.dat")
        .then(function (file) {
            return Windows.Storage.FileIO.readBufferAsync(file);
        }).done(function (buffer) {
            console.log("Read from credbuffer.dat");
            launchCredPicker(buffer);
        }, function (e) {
            console.log("Could not reopen credbuffer.dat; launching default");
            launchCredPicker(null);
        });
}
```
```