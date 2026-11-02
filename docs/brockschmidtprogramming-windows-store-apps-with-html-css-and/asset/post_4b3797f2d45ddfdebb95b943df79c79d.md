
You can test all this by running the HereMyAm! app, taking a suitable picture and making sure you have a location. Then use the Suspend and Shutdown option on the Visual Studio toolbar to terminate the app. Set a breakpoint on the updatePosition call above, and then restart the app in the debugger. You'll see that sessionState.lastPosition is initialized at that point.

With the last captured picture, we don't need to save the StorageFile, just the URI: we copied the file into our local appdata (so it persists across sessions already) and can just use the ms-appdata:// URI scheme to refer to it. When we capture an image, we just save that URI into sessionState.imageURI (the property name is arbitrary) at the end of the promise chain inside capturePhoto:

```
app.sessionState.imageURI = "ms-appdata:///local/HereMyAm/" + newFile.name;
```

Again, because imageURI is saved within sessionState, this value will be available when the app is restarted after being terminated. We also need to re-initialize lastCapture with a StorageFile so that the image is available through the Share contract. For this we can use Windows.Storage.StorageFile.getFileFromApplicationUriAsync. Here, then, is the code within the previousExecutionState == terminated case during activation:

```
// WinJS reloads the sessionState object here: initialize from the saved image URI and location.
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

Note: Using ms-appdata:/// and getFileFromApplicationUriAsync (or its sibling getFileFromPathAsync) works because the file exists in a location that we can access programmatically by default. It also works for libraries for which we declare a capability in the manifest. If, however, we obtain a StorageFile from the file picker, we need to save that in the Windows.Storage.AccessCache to preserve access permissions across sessions. We'll revisit the access cache in Chapter 11, "The Story of State, Part 2."

## Page Controls and Navigation

Now we come to an aspect of Windows Store apps that very much separates them from typical web applications but makes them very similar to AJAX-based sites.

To compare, many web applications do page-to-page navigation with `<a href>` hyperlinks or by setting `document.location` from JavaScript. This is all well and good: oftentimes there's little or no state to pass between pages, and even then there are well-established mechanisms for doing so, such as HTML5 `sessionStorage` and `localStorage` (which work just fine in Store apps, by the way).

This type of navigation presents a few problems for Store apps, however. For one, navigating to a new page means a wholly new script context—all the JavaScript variables from your previous page will be lost. Sure, you can pass state between those pages, but managing this across an entire app likely hurts performance and can quickly become your least favorite programming activity. It's better and easier, in other words, for client apps to maintain a consistent in-memory state across pages and also have each individual page be able to load what script it uniquely needs, as needed.

Also, the nature of the HTML/CSS rendering engine is such that a blank screen appears when navigating a hyperlink. Users of web applications are accustomed to waiting a bit for a browser to acquire a new page (I've found many things to do with an extra 15 seconds!), but this isn't an appropriate user experience for a fast and fluid Windows Store app. Furthermore, such a transition doesn't allow animation of various elements on and off the screen, which can help provide a sense of continuity between pages if that fits with your design.

So, although you can use direct links, Store apps typically implement "pages" by dynamically replacing sections of the DOM within the context of a single page like default.html, akin to how "single-page" web applications work. By doing so, the script context is always preserved and individual elements or groups of elements can be transitioned however you like. In some cases, it even makes sense to simply show and hide pages so that you can switch back and forth quickly. Let's look at the strategies and tools for accomplishing these goals.

### WinJS Tools for Pages and Page Navigation

Windows itself, and the app host, provide no mechanism for dealing with pages—from the system's perspective, this is merely an implementation detail for apps to worry about. Fortunately, the engineers who created WinJS and the templates in Visual Studio and Blend worried about this a lot! As a result, they've provided some marvelous tools for managing bits and pieces of HTML+CSS+JS in the context of a single container page:

- `WinJS.UI.Fragments` contains a low-level "fragment-loading" API, the use of which is necessary only when you want close control over the process (such as which parts of the HTML fragment get which parent). We won't cover it in this book; see the documentation and the Loading HTML fragments sample.

- `WinJS.UI.Pages` is a higher-level API intended for general use and is employed by the templates. Think of this as a generic wrapper around the fragment loader that lets you easily define a "page control"—simply an arbitrary unit of HTML, CSS, and JS—that you can easily pull into the context of another page as you do other controls.²¹ They are, in fact, implemented like other controls in WinJS (as we'll see in Chapter 5), so you can declare them in markup, instantiate them with WinJS.UI.processAll, use as many of them within a single host page as you like, and even nest them.

These APIs provide only the means to load and unload individual "pages"—they pull HTML in from other files (along with referenced CSS and JS) and attach the contents to an element in the DOM. That's it. As such they can be used for any number of purposes, such as a custom control model, depending on how you like to structure your code. See scenario 1 of the HTML Page controls sample.

### Page controls and fragments are not gospel

To be clear, there's absolutely no requirement that you use the WinJS mechanisms described here in a Windows Store app. These are simply convenient tools for common coding patterns. In the end, it's just about making the right elements and content appear in the DOM for your user experience, and you can implement that however you like.

Assuming that you'll want to save yourself loads of trouble and use WinJS for page-to-page navigation, you'll need two other pieces. The first is something to manage a navigation stack, and the second is something to hook navigation events to the loading mechanism of WinJS.UI.Pages.

For the first piece, you can turn to WinJS.Navigation, which supplies, through about 150 lines of CS101-level code, a basic navigation stack. This is all it does. The stack itself is just a list of URIs on top of which WinJS.Navigation exposes location, history, canGoBack, and canGoForward properties, along with one called state in which you can store any app-defined object you need. The stack (maintained in history) is manipulated through the forward, back, and navigate methods, and the WinJS.Navigation object raises a few events—beforenavigate, navigating, and navigated—to anyone who wants to listen (through addEventListener).²²

Tip: In the WinJS.Navigation.history.current there's an initialPlaceholder flag that answers the question, "Can WinJS.Navigation.navigate go to a new page without adding an entry in the history?" If you set this flag to true, subsequent navigations won't be stored in the nav stack. Be sure to set it back to false to reenable the stack.

What this means is that WinJS.Navigation by itself doesn't really do anything unless some other piece of code is listening to those events. That is, for the second piece of the navigation puzzle we need a linkage between WinJS.Navigation and WinJS.UI.Pages, such that a navigation event causes the
