A page control is essentially just an object with some standard methods. You can instantiate the control from JavaScript with `new` by first obtaining its constructor function from `WinJS.UI.Pages.get(<page_uri>)` and then calling that constructor with the parent element and an object containing its options. This operation already encapsulated within `WinJS.UI.Pages.render`, as we'll see shortly.

Although a basic structure for the `ready` method is provided by the templates, `WinJS.UI.Pages` and the `PageControlNavigator` will make use of the following if they are available, which are technically the members of an interface called `WinJS.UI.IPageControlMembers`:

| PageControl Method | When Called |
| --- | --- |
| `init` | Called before elements from the page control have been created. |
| `processed` | Called after `WinJS.UI.processAll` is complete (that is, controls in the page have been instantiated, which is done automatically), but before page content itself has been added to the DOM. Once you return from this method—or promise you return is fulfilled—WinJS animates the new page into view with `WinJS.UI.Animation.enterPage`, so all initialization of properties and data-binding should occur within this method. |
| `ready` | Called after the page has been added to the DOM. |
| `error` | Called if an error occurs in loading or rendering the page. |
| `unload` | Called when navigation has left the page. By default, WinJS automatically disposes of controls on a page when that page is unloaded; see "Sidebar: The Ubiquitous dispose Method" in Chapter 5. |
| `updateLayout` | Called in response to the `window.onresize` event, which signals changes between various view states. |

Note that `WinJS.UI.Pages` calls the first four methods; the `unload` and `updateLayout` methods, on the other hand, are used only by the `PageControlNavigator`.

Of all of these, the `ready` method is the most common one to implement. It's where you'll do further initialization of controls (e.g., populate lists), wire up other page-specific event handlers, and so on. Any processing that you want to do before the page content is added to the DOM should happen in `processed`, and note that if you return a promise from `processed`, WinJS will wait until that promise is fulfilled before starting the enterpage animation.

The `unload` method is also where you'll want to remove event listeners for WinRT objects, as described earlier in this chapter in "WinRT Events and removeEventListener." The `updateLayout` method is important when you need to adapt your page layout to a new view, as we've been doing in the Here My Am! app.

As for the `PageControlNavigator` itself, which I'll just refer to as the "navigator," the code in `js/navigator.js` shows how it's defined and how it wires up navigation events in its constructor:

```
~~~javascript
(function () {
    "use strict";

    // [some bits omitted]
    var nav = WinJS.Navigation;

    WinJS.Namespace.define("Application", {
~~~
```