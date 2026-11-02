
```
~~~javascript
// Display the body as HTML (item.content is a SyndicationContent object, item.summary is
// a SyndicationText object).
var content = "(no content)";
if (item.content) {
    content = item.content.text;
}
else if (item.summary) {
    content = item.summary.text;
}
document.getElementById("scenario1WebView").innerHTML = window.toStaticHTML(content);

// Display element extensions. The elementExtensions collection contains all the additional
// child elements within the current element that do not belong to the Atom or RSS standards
// (e.g., Dublin Core extension elements). By creating an array of these, we can create a
// WinJS.Binding.List that's easily displayed in a ListView.
var bindableNodes = [];
for (var i = 0; i < item.elementExtensions.size; i++) {
    var bindableNode = {
        nodeName: item.elementExtensions[i].nodeName,
        nodeNamespace: item.elementExtensions[i].nodeNamespace,
        nodeValue: item.elementExtensions[i].nodeValue,
    };
    bindableNodes.push(bindableNode);
}
var dataList = new WinJS.Binding.List(bindableNodes);
var listView = document.getElementById("extensionsListView").winControl;
WinJS.UI.setOptions(listView, { itemDataSource: dataList.dataSource });
}
~~~
```

It's probably obvious that the API, under the covers, is probably just using the XmlDocument API to retrieve all these properties. In fact, its getXmlDocument returns that XmlDocument if you want to access it yourself.

You can also create a SyndicationFeed object around the XML for a feed you might already have. For example, if you obtain the feed contents by using WinJS.xhr, you can create a new SyndicationFeed object and call its load method with the request's responseXML. Then you can work with the feed through the class hierarchy. When using the Windows.Web.AtomPub API to manage a feed, you also create a new or updated SyndicationItem to send across the wire, settings its values through the other objects in its hierarchy. We'll see this in the next section.

If retrieveFeedAsync throws an exception, by the way, which would be picked up by an error handler you provide to the promise's done method, you can turn the error code into a SyndicationErrorStatus value. Here's how it's used in the sample's error handler:

```
~~~javascript
function onError(err) {
    // Match error number with a SyndicationErrorStatus value. Use
    // Windows.Web.WebErrorStatus.getStatus() to retrieve HTTP error status codes.
    var errorStatus = Windows.Web.Syndication.SyndicationError.getStatus(err.number);
    if (errorStatus === Windows.Web.Syndication.SyndicationErrorStatus.invalidXml) {
        displayLog("An invalid XML exception was thrown. Please make sure to use a URI that"
            + " points to a RSS or Atom feed.");
    }
}
~~~
```

```
~~~
}
~~~
```

As a final note, the Feed reader sample in the SDK provides another demonstration of the Windows.Web.Syndication API. Its operation is fully described on the Feed reader sample page in the documentation.

## Using AtomPub

On the flip side of reading an RSS feed, as we've just seen, is the need to possibly add, remove, and edit entries on a feed, as with an app that lets the user actively manage a specific blog or site.

The API for this is found in Windows.Web.AtomPub and demonstrated in the AtomPub sample. The main class is the AtomPubClient that encapsulates all the operations of the AtomPub protocol. It has methods like createResourceAsync, retrieveResourceAsync, updateResourceAsync, and deleteResourceAsync for working with those entries, where each resource is identified with a URI and a SyndicationItem object, as appropriate. Media resources for entries are managed through createMediaResourceAsync and similarly named methods, where the resource is provided as an IInputStream.

The AtomPubClient also has retrieveFeedAsync and setRequestHeader methods that do the same as the SyndicationClient methods of the same names, along with a few similar properties like serverCredential, timeout, and bypassCacheOnRetrieve. Another method, retrieveServiceDocumentAsync, provides the workspace/service documents for the feed (in the form of a Windows.Web.AtomPub.ServiceDocument object).

Again, the AtomPub sample demonstrates the different operations: retrieve (Scenario 1), create (Scenario 2), delete (Scenario 3), and update (Scenario 4). Here's how it first creates the AtomPubClient object (see *js/common.js*), assuming there are credentials:

```
~~~javascript
function createClient() {
    client = new Windows.Web.AtomPub.AtomPubClient();
    client.bypassCacheOnRetrieve = true;

    var credential = new Windows.Security.Credentials.PasswordCredential();
    credential.userName = document.getElementById("userNameField").value;
    credential.password = document.getElementById("passwordField").value;
    client.serverCredential = credential;
}
~~~
```

Updating an entry (*js/update.js*) then looks like this, where the update is represented by a newly created SyndicationItem:

```
~~~javascript
function getCurrentItem() {
    if (currentFeed) {
        return currentFeed.items[currentItemIndex];
    }
    return null;
}
~~~
```

![](img/0e8e4a2b6f953d3397e14e88cd5d8b4d_744_0.png)

The result from `pickAsync`, as given to your completed handler, is a `CredentialPickerResults` object with the following properties (when you enter some credentials in the sample, you'll see these values reflected in the sample's output):

- `credentialUserName` A string containing the entered username.
- `credentialPassword` A string containing the password (typically encrypted depending on the authentication protocol option).
- `credentialDomainName` A string containing a domain if entered with the username (as in `<domain>\<username>`).
- `credentialSaved` A Boolean indicating whether the credential was saved automatically; this depends on picker options, as discussed below.
- `credentialSavedOption` A `CredentialSavedOption` value indicating the state of the Remember My Credentials check box: `unselected`, `selected`, or `hidden`.
- `errorCode` Contains zero if there is no error, otherwise an error code.
- `credential` An `IBuffer` containing the credential as an opaque byte array. This is what you can save in your own persistent state if need be and pass back to the picker at a later time. We'll see how at the end of this section.

The three scenarios in the sample demonstrate the different options you can use to invoke the credential picker. For there are three separate variants of `pickAsync`. The first variant accepts a target name (which is ignored) and a message string that appears in the place of “Please enter your credentials” shown in the previous screen shot:

```
```
Windows.Security.Credentials.UI.CredentialPicker.pickAsync(targetName, message)
    .done(function (results) {
    })
```
```

The second variant accepts the same arguments plus a caption string that appears in the place of "Credential Picker Sample" in the screen shot:

```
```
Windows.Security.Credentials.UI.CredentialPicker.pickAsync(targetName, message, caption)
    .done(function (results) {
    })
```
```

The third variant accepts a `CredentialPickerOptions` object that has properties for the same `targetName`, `message`, and `caption` strings, along with the following:

- `previousCredential`  An `IBuffer` with the opaque credential information as provided by a previous invocation of the picker (see `CredentialPickerResults.credential` above).
- `alwaysDisplayDialog`  A Boolean indicating whether the picker is displayed. The default is `false`, but this applies only if you also populate `previousCredential` (with an exception for domain-joined machines—see table below). The purpose here is to show the dialog when a stored credential might be incorrect and the user is expected to provide a new one.
- `errorCode`  The numerical value of a Win32 error code (default is `ERROR_SUCCESS`) that will be formatted and displayed in the dialog box. You would use this when you obtain credentials from the picker initially but find that those credentials don't work and need to invoke the picker again. Instead of providing your own message, you just choose an error code and let the system do the rest. The most common values for these are 1326 (login failure), 1330 (password expired), 2202 (bad username), 1907 or 1938 (password must change/password change required), 1351 (can't access domain info), and 1355 (no such domain). There are, in fact, over 15,000 Win32 error codes, but that means you'll have to search the reference linked above (or search within the winerror.h file typically found in your Program Files (x86)\Windows Kits\8.0\Include\shared folder). Happy hunting!
- `callerSavesCredential`  A Boolean indicating that the app will save the credential and that the picker should not. The default value is `false`. When set to `true`, credentials are saved to a secure system location (not the credential locker) if the app has the *Enterprise Authentication* capability (see below).
- `credentialSaveOption`  A `CredentialSaveOption` value indicating the initial state of the Remember My Credentials check box: unselected, selected, or hidden.
- `authenticationProtocol`  A value from the `AuthenticationProtocol` enumeration: `basic`, `digest`, `ntlm`, `kerberos`, `negotiate` (the default), `credSsp`, and `custom` (in which case you must supply a string in the `customAuthenticationProtocol` property). Note that with `basic` and `digest`, the `CredentialPickerResults.credentialPassword` will not be encrypted and is subject to the same security needs as a plain text password you collect from your own UI.

Here's an example of invoking the picker with an `errorCode` indicating a previous failed login:
