![](bbox=[0.15, 0.085, 0.85, 0.421])

**FIGURE 4-2** Displaying a webview, which is an HTML element like any others within an app layout. The webview runs within the web context and allows navigation within its own content.

Clicking links inside a webview will navigate to those pages. In many cases with live web pages, you’ll see JavaScript exceptions if you’re running the app in the debugger. Such exceptions will not terminate the app as a whole, so they can be safely ignored or left unhandled. Outside of the debugger, in fact, a user will never see these—the webview ignores them.

As we see in this example, setting the `src` attribute is one way to load content into the webview. The webview object also supports four other methods:

+   - `navigate` Navigates the webview to a supported URI ([http[s], ms-appx-web, and ms-appdata). That page can contain references to other URIs except for `ms-appx`.
+   - `navigateWithHttpRequestMethod` Navigates to a supported URI with the ability to set the HTTP verb and headers.
+   - `navigateToString` Renders an HTML string literal into the webview. References can again refer to supported URIs except for `ms-appx`.
+   - `navigateToLocalStreamUri` Navigates to a page in local appdata using an app-provided object to resolve relative URIs and possibly decrypt the page content.

Examples of the most of these can be found in the HTML Webview control sample. Scenario 1 shows `navigate`, starting with an empty webview and then calling `navigate` with a URI string (`js/1_NavToUrl.js`):