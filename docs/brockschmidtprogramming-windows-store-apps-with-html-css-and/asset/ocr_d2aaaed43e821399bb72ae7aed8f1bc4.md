source can refer to an app's in-package logo. (Such a page, of course, would not work in a browser)

+   * The local context has access to the WinRT API, among other things, but cannot load remote script (referenced via `http://`); the web context is allowed to load and execute remote script but cannot access WinRT.
+   * ActiveX control plug-ins are generally not allowed in either context and will fail to load in both `iframe` and `webview` elements. The few exceptions are noted on `Migrating a web app`.
+   * In the local context, strings assigned to `innerHTML`, `outerHTML`, `adjacentHTML`, and other properties where script injection can occur, as well as strings given to `document.write` and similar methods, are filtered to remove script. This does not happen in the web context.
+   * Every `iframe` and `webview` element—in either context—has its own JavaScript global namespace that's entirely separate from that of the parent page. Neither can access the other.
+   * The HTML5 `postMessage` function can be used to communicate between an `iframe` and its containing parent across contexts, with a webview such communication happens with the `invokeScriptAsync` method and `window.external.notify`. These capabilities can be useful to execute remote script within the web context and pass the results to the local context; script acquired in the web context should not itself be passed to the local context and executed there. (Again, Windows Store policy disallows this, and apps submitted to the Store are analyzed for such practices.)
+   * Further specifics can be found on `Features and restrictions by context`, including which parts of WinJS don't rely on WinRT and can thus be used in the web context. (WinJS, by the way, is not supported for use on web pages outside of an app, just the web context within an app.)

An app's home page—the one you point to in the manifest in the Application > Start Page field—always runs in the local context, and any page to which you navigate directly (via `<a href>` or `document.location`) must also be in the local context. When using page controls to load HTML fragments into your home page, those fragments are of course rendered into the local context.

Next, a local context page can contain any number of `webview` and `iframe` elements. For the webview, because it always loads its content in the web context and cannot refer to `ms-appx` URIs, it pretty much acts like an embedded web browser where navigation is concerned.

Each `iframe` element, on the other hand, can load in-package content in either local or web context. (By the way, programmatic read-only access to your package contents is obtained via `Windows.ApplicationModel.Package.Current.InstalledLocation`.) Referring to a remote location (https) will always place the `iframe` in the web context.

Here are some examples of different URIs and how they get loaded in an `iframe`:

```
```html
<!-- iframe in local context with source in the app package -->
<!-- these forms are allowed only from inside the local context -->
<iframe src="/frame-local.html"></iframe>
```
```