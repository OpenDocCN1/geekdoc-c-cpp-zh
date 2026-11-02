
Scenario 3 of that same sample demonstrates how calls to WinRT APIs are allowed in the local context but blocked in the web context. It loads the same page, callWinRT.html, into a separate iframe in each context, which also means the same JavaScript is loaded (and isolated) in both. When running this scenario you can see that WinRT calls will fail in the web context.

A good tip to pick up from this sample is that you can use the document.location.protocol property to check which context you're running in, as done in js/callWinRT.js:

```
var isWebContext = (document.location.protocol === "ms-appx-web:");
```

Checking against the string "ms-appx:" will, of course, tell you if you're running in the local context.

Scenarios 5 and 6 of the sample are very interesting because they help us explore matters around inserting HTML into the DOM and navigating from the web to the local context. Each of these subjects, however, needs a little more context of their own (forgive the pun!), as discussed in the next two sections.

**Tip** To prevent selection of content in an iframe, style the iframe with -ms-user-select: none or set its style.msUserSelect property to "none" in JavaScript. This does not, however, work for the webview control; its internal content would need to be styled instead.

## Dynamic Content

As we've seen, the ms-appx and ms-appx-web schema allow an app to navigate iframe and webview elements to pages that exist inside the app package. This begs a question: can an app point to content on the local file system that exists outside the app package, such as a dynamically created file in an appdata folder? Can, perchance, an app use the file:// protocol to navigate to and/or access that content?

Well, as much as I'd love to tell you that this just works, the answer is somewhat mixed. First, the file protocol—along with custom protocols—are wholly blocked by design for various security reasons, even for your appdata folders to which you otherwise have full access. Fortunately, there is a substitute, ms-appdata:///, that fulfills part of the need (the third / again allows you to omit the specific package name). Within the local context of an app, ms-appdata is a shortcut to your appdata folder wherein exist local, roaming, and temp folders. So, if you created a picture called image65.png in your appdata local folder, you can refer to it by using ms-appdata:///local/image65.png. Similar forms work with roaming and temp and work wherever a URI can be used, including within a CSS style like background.

Within iframes, ms-appdata can be used only for resources, namely with the src attribute of img, video, and audio elements. It cannot be used to load HTML pages, CSS stylesheets, or JavaScript, nor can it be used for navigation purposes (iframe, hyperlinks, etc.). This is because it wasn't feasible to create a sub-sandbox environment for such pages, without which it would be possible for a page loaded with ms-appdata to access everything in your app. Fortunately, you can navigate a webview to app data content, as we'll see shortly, thereby allowing you to generate and display HTML pages dynamically without having to write your own rendering engine (whew!).

You can also load bits of HTML, as we've seen with page controls, and insert that markup into the DOM through `innerHTML`, `outerHTML`, `insertAdjacentHTML` and related properties, as well as `document.write` and `DOMParser.parseFromString`. But remember that automatic filtering is applied in the local context to prevent injection of script and other risky markup (and if you try, the app host will throw exceptions, as will `WinJS.Utilities.setInnerHTML`, `setOuterHTML`, and `insertAdjacentHTML`). This is not a concern in the web context, of course.

This brings us to whether you can generate and execute script on the fly in the local context at all. The answer is again qualified. Yes, you can take a JavaScript string and pass it to the `eval` or `execScript` functions, even inject script through properties like `innerHTML`. But be mindful again of Windows Store certification requirement 3.9 that specifically disallows dynamic script that changes your app logic or its interaction with WinRT.

That said, there are situations where you, the developer, really know what you're doing and enjoy juggling chainsaws and flaming swords (or maybe you're just trying to use a third-party library; see the sidebar below). Acknowledging that, Microsoft provides a mechanism to consciously circumvent script filtering: `MSApp.execUnsafeLocalFunction`. For all the details regarding this, refer to Developing secure apps, which covers this along with a few other obscure topics that I'm not including here (like the numerous variations of the `sandbox` attribute for `iframes`, which is also demonstrated in the JavaScript iframe sandbox attribute sample).

And curiously enough, WinJS actually makes it easier for you to juggle chainsaws and flaming swords! `WinJS.Utilities.setInnerHTMLUnsafe`, `setOuterHTMLUnsafe`, and `insertAdjacentHTMLUnsafe` are wrappers for calling DOM methods that would otherwise strip out risky content. Alternatively, if you want to sanitize HTML before attempting to inject it into an element (and thereby avoid exceptions), you can use the `toStaticHTML` method, as demonstrated in scenario 5 of the Integrating content and control from web services sample.

## Sidebar: Third-Party Libraries and the Hosted Environment

In general, Windows Store apps can employ libraries like jQuery, Prototype, Dojo, and so forth, as noted in Chapter 1. However, there are some limitations and caveats.

First, because local context pages in an app cannot load script from remote sources, apps typically need to include such libraries in their packages unless they're only being used from the web context. WinJS, mind you, doesn't need bundling because it's provided by the Windows Store, but such "framework packages" are not enabled for third parties.

Second, DOM API changes and app container restrictions might affect the library. For example, using `window.alert` won't work. One library also cannot load another library from a remote source in the local context. Crucially, anything in the library that assumes a higher level of trust than the app container provides (such as open file system access) will have issues.

The most common problem comes up when libraries inject elements or script into the DOM (as through `innerHTML`), a widespread practice for web applications that is not automatically allowed within the app container. You can get around this on the app level by wrapping code within `MSApp.execUnsafeLocalFunction`, but that doesn't solve injections coming from deeper inside the library. In these cases you really need to work with the library author.

In short, you're free to use third-party libraries so long as you're aware that they might have been written with assumptions that don't always apply within the app container. Over time, of course, fully Windows-compatible versions of such libraries, like `jQuery 2.0`, will emerge. Note also that for any libraries that include binary components, those must be targeted to Windows 8.1 for use with a Windows 8.1 app.

## App Content URIs

When drawing on a variety of web content, it's important to understand the degree to which you trust that content. That is, there's a huge difference between web content that you control and that which you do not, because by bringing that content into the app, the app essentially takes responsibility for it. This means that you want to be careful about what privileges you extend to that web content. In an `iframe`, those privileges include cross-context navigation, geolocation, IndexedDB, HTML5 AppCache, clipboard access, and navigating to web content with an `https` URI. In a webview, it means the ability for remote content to raise an event to the app.

If you ask nicely, in other words, Windows will let you enable such privileges to web pages that the app knows about. All it takes is an affidavit signed by you and sixteen witnesses and...OK, I'm only joking! You simply need to add what are called *application content URI rules* to your manifest in the Content Uri tab. Each rule—composed of an exact `https` URI or one with wildcards (*)—says that content from some URI is known and trusted by your app and can thus act on the app's behalf. You can also exclude URIs, which is typically done to exclude specific pages that would otherwise be allowed by another rule.

For instance, the very simple ContentUri example in this chapter's companion content has an `iframe` pointing to `https://www.bing.com/maps/` (Bing allows an `https://` connection), and this URI is included in the content URI rules. This allows the app to host the remote content as partially shown below. Now click or tap the geolocation crosshair circle on the upper left of the map next to World. Because the rules say we trust this content (and trust that it won't try to trick the user), a geolocation request invokes a consent dialog (as shown below) just as if the request came from the app. (Note: When run inside the debugger, the ContentUri example will probably show exceptions on startup. If so, press Continue within Visual Studio; this doesn't affect the app running outside the debugger.)
