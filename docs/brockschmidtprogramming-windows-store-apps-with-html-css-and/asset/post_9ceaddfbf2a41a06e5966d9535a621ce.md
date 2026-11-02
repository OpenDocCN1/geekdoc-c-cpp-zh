
**Caution** `iframe` and `x-ms-webview` elements are not intended to let you just build an app out of remote web pages. Section 2 of the Windows Store app certification requirements, in fact, specifically disallows this: "the primary app experience must take place within the app," meaning that it doesn't happen within hosted websites. A few key reasons for this are that many websites aren't set up well for touch interaction (which violates requirement 3.5) and often won't work well in different views (violating requirement 3.6). You also want to make sure that the user can navigate easily without getting lost in random websites and that the app still follows the design guidelines, uses the app bar, supports contracts like Share, and so on.

In short, overuse of web content will likely mean that the app won't be accepted by the Store, though web content that's specifically designed for use with an app and behaves like native app content won't be so scrutinized.

Requirement 3.9 also disallows dynamically downloading code or data that changes how the app interacts with the WinRT API. This is admittedly a bit of a gray area, as downloading data to configure a game level, for instance, doesn't quite fall into this category. Nevertheless, this requirement is taken seriously so be very careful about making assumptions here.

## Local and Web Contexts (and iframe Elements)

As described in Chapter 1, "The Life Story of a Windows Store App," apps written with HTML, CSS, and JavaScript are not directly executable like their compiled counterparts written in C#, Visual Basic, or C++. In our app packages, there are no EXEs, just `.html`, `.css`, and `.js` files that are, plain and simple, nothing but text. So something has to turn all this text that defines an app into something that's actually running in memory. That something is again the app host, `wwahost.exe`, which creates what we call the *hosted environment* for Store apps.

Let's review what we've already learned in Chapters 1 and 2 about the characteristics of the hosted environment:

- The app host (and the apps in it) use brokered access to sensitive resources, controlled both by declared capabilities in the manifest and run-time user consent.
- Though the app host provides an environment very similar to that of Internet Explorer (10+), there are a number of changes to the DOM API, documented on HTML and DOM API changes list and HTML, CSS, and JavaScript features and differences. A related topic is Windows Store apps using JavaScript versus traditional web apps.
- HTML content in the app package can be loaded into the *local* or *web* context, depending on the hosting element. `iframe` elements can use the `ms-appx://` scheme to refer to in-package pages loaded in the local context or `ms-appx-web://` to specify the web context. (The third slash again means "in the app package"; the Here My Am! app uses this to load its `map.html` file into a web context `iframe`.) Remote `https` content in an `iframe` and all content in a `webview` always runs in the web context.
- Any content within a web context can refer to in-package resources (such as images and other media) with `ms-appx-web` URIs. For example, a page loaded into a `webview` from an `http` source can refer to an app's in-package logo. (Such a page, of course, would not work in a browser.)
- The local context has access to the WinRT API, among other things, but cannot load remote script (referenced via `http://`); the web context is allowed to load and execute remote script but cannot access WinRT.
- ActiveX control plug-ins are generally not allowed in either context and will fail to load in both `iframe` and `webview` elements. The few exceptions are noted on `Migrating a web app`.
- In the local context, strings assigned to `innerHTML`, `outerHTML`, `adjacentHTML`, and other properties where script injection can occur, as well as strings given to `document.write` and similar methods, are filtered to remove script. This does not happen in the web context.
- Every `iframe` and `webview` element—in either context—has its own JavaScript global namespace that's entirely separate from that of the parent page. Neither can access the other.
- The HTML5 `postMessage` function can be used to communicate between an `iframe` and its containing parent across contexts; with a `webview`, such communication happens with the `invokeScriptAsync` method and `window.external.notify`. These capabilities can be useful to execute remote script within the web context and pass the results to the local context; script acquired in the web context should not itself be passed to the local context and executed there. (Again, Windows Store policy disallows this, and apps submitted to the Store are analyzed for such practices.)
- Further specifics can be found on `Features and restrictions by context`, including which parts of WinJS don't rely on WinRT and can thus be used in the web context. (WinJS, by the way, is not supported for use on web pages outside of an app, just the web context within an app.)

An app's home page—the one you point to in the manifest in the Application > Start Page field—always runs in the local context, and any page to which you navigate directly (via `<a href>` or `document.location`) must also be in the local context. When using page controls to load HTML fragments into your home page, those fragments are of course rendered into the local context.

Next, a local context page can contain any number of `webview` and `iframe` elements. For the webview, because it always loads its content in the web context and cannot refer to `ms-appx` URIs, it pretty much acts like an embedded web browser where navigation is concerned.

Each `iframe` element, on the other hand, can load in-package content in either local or web context. (By the way, programmatic read-only access to your package contents is obtained via `Windows.ApplicationModel.Package.Current.InstalledLocation`.) Referring to a remote location (https) will always place the `iframe` in the web context.

Here are some examples of different URIs and how they get loaded in an `iframe`:

```html
<!-- iframe in local context with source in the app package -->
<!-- these forms are allowed only from inside the local context -->
<iframe src="/frame-local.html"></iframe>

<iframe src="ms-appx:///frame-local.html"></iframe>

<!-- iframe in web context with source in the app package -->
<iframe src="ms-appx-web:///frame-web.html"></iframe>

<!-- iframe with an external source automatically assigns web context -->
<iframe src="https://my.secure.server.com/"></iframe>
```

Also, if you use an `<a href="..." target="...">` tag with `target` pointing to an `iframe`, the scheme in `href` determines the context. And once in the web context, an `iframe` can host only other web context `iframe`s such as the last two above; the first two elements would not be allowed.

**Tip** Some web pages contain frame-busting code that prevents the page from being loaded into an `iframe`, in which case the page will be opened in the default browser and not the app. In this case, use a `webview` if you can; otherwise you'll need to work with the site owner to create an alternate page that will work for you.

Although Windows Store apps typically don't use `<a href>` or `document.location` for page navigation, similar rules apply if you do happen to use them. The whole scene here, though, can begin to resemble overcooked spaghetti, so I've simplified the exact behavior for these variations and for iframes in the following table:

| Target | Result in Local Context Page | Result in Web Context Page |
|---|---|---|
| `<iframe src="ms-appx:///"></iframe>` | `iframe` in local context | Not allowed |
| `<iframe src="ms-appx-web:///"></iframe>` | `iframe` in web context | `iframe` in web context |
| `<iframe src="https://...">` | `iframe` in web context | `iframe` in web context |
| `<a href="[uri]" target="myFrame">` `<a name="myFrame">` | `iframe` in local or web context depending on [uri] | `iframe` in web context; [uri] cannot begin with ms-appx... |
| `<a href="ms-appx:///...">` | Links to page in local context | Not allowed unless explicitly specified (see below) |
| `<a href="ms-appx-web:///...">` | Not allowed | Links to page in web context |
| `<a href="[uri]">` with any other protocol including http[s] | Opens default browser with [uri] | Opens default browser with [uri] |

The last two items in the table really mean that a Windows Store app cannot navigate from its top-level page (in the local context) directly to a web context page of any kind (local or remote) and remain within the app—the app host will launch the default browser instead. That's just life in the app host! Such content must be placed in an `iframe` or a `webview`. Similarly, navigating from a web context page to a local context page is not allowed by default but can be enabled, as we'll see shortly.

In the meantime, let's see a few simpler iframe examples. Again, in the Here My Am! app we've already seen how to load an in-package HTML page in the web context and communicate with the parent page through `postMessage` (We'll change this to a `webview` in a later section.) Very similar and more isolated examples can also be found in scenarios 2 and 4 of the Integrating content and controls from web services sample.
