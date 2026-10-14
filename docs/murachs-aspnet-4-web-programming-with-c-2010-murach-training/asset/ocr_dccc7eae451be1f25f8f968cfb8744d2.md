# Methods that set page caching options

| Method | Description |
|---|---|
| `Response.Cache.SetCacheability` | Indicates how the page should be cached. Specify `HttpCacheability.NoCache` to suppress caching. |
| `Response.Cache.SetExpires` | Specifies when the cached page should expire. Specify `Now().AddSeconds(-1)` to mark the page as already expired. |
| `Response.Cache.SetNoStore` | Specifies that the browser should not cache the page. |
| `Response.AppendHeader` | Adds a header to the HTTP response object. Specifying “Pragma” for the key and “no-cache” for the value disables caching. |

# Code that disables caching for a page

```
Response.Cache.SetCacheability(HttpCacheability.NoCache);
Response.Cache.SetExpires(Now.AddSeconds(-1));
Response.Cache.SetNoStore();
Response.AppendHeader("Pragma", "no-cache");
```

# Description

+   - You can limit the effect of the Back button by directing the browser to not cache pages that contain state-sensitive data. Then, when the user attempts to return to a page using the Back button, the page may be reloaded or a warning message may be displayed indicating that the page has expired. If a warning message is displayed, the user can click the Refresh button to reload the page.
+   - You can place the code to disable browser page caching in the method that handles the Load event of the page. This code should be executed each time the page is loaded.
+   - Unfortunately, the technique described in this figure doesn’t work with all browsers. As a result, you may want to use the technique in the next figure to prevent back-button problems.