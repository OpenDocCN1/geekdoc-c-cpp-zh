Scenario 3 of that same sample demonstrates how calls to WinRT APIs are allowed in the local context but blocked in the web context. It loads the same page, callWinRT.html, into a separate iframe in each context, which also means the same JavaScript is loaded (and isolated) in both. When running this scenario you can see that WinRT calls will fail in the web context.

A good tip to pick up from this sample is that you can use the document.location.protocol property to check which context you're running in, as done in js/callWinRT.js:

```
var isWebContext = (document.location.protocol === "ms-appx-web:");
```

Checking against the string "ms-appx:" will, of course, tell you if you're running in the local context.

Scenarios 5 and 6 of the sample are very interesting because they help us explore matters around inserting HTML into the DOM and navigating from the web to the local context. Each of these subjects, however, needs a little more context of their own (forgive the pun!), as discussed in the next two sections.

**Tip** To prevent selection of content in an iframe, style the iframe with -ms-user-select: none or set its style.msUserSelect property to "none" in JavaScript. This does not, however, work for the webview control; its internal content would need to be styled instead.

# Dynamic Content

As we've seen, the ms-appx and ms-appx-web schema allow an app to navigate iframe and webview elements to pages that exist inside the app package. This begs a question: can an app point to content on the local file system that exists outside the app package, such as a dynamically created file in an appdata folder? Can, perchance, an app use the file:// protocol to navigate to and/or access that content?

Well, as much as I'd love to tell you that this just works, the answer is somewhat mixed. First, the file protocol—along with custom protocols—are wholly blocked by design for various security reasons, even for your appdata folders to which you otherwise have full access. Fortunately, there is a substitute, ms-appdata:///, that fulfills part of the need (the third /again allows you to omit the specific package name). Within the local context of an app, ms-appdata is a shortcut to your appdata folder wherein exist local, roaming, and temp folders. So, if you created a picture called image65.png in your appdata local folder, you can refer to it by using ms-appdata:///local/image65.png. Similar forms work with roaming and temp and work wherever a URI can be used, including within a CSS style like background

Within iframes, ms-appdata can be used only for resources, namely with the src attribute of img, video, and audio elements. It cannot be used to load HTML pages, CSS stylesheets, or JavaScript, nor can it be used for navigation purposes (iframe, hyperlinks, etc.). This is because it wasn't feasible to create a sub-sandbox environment for such pages, without which it would be possible for a page loaded with ms-appdata to access everything in your app. Fortunately, you can navigate a webview to app data content, as we'll see shortly, thereby allowing you to generate and display HTML pages dynamically without having to write your own rendering engine (whew!).