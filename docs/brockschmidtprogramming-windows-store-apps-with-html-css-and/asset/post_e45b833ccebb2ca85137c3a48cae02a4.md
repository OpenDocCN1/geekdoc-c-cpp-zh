
The `getAsync` method creates a generic HTTP GET request. Its `message` argument is an `HttpRequestMessage` object, where you can construct whatever type of request you need, setting the `requestUri`, `headers`, `transportInformation`,<sup>37</sup> and other arbitrary `properties` that you want to communicate to the filter and possibly the server. The completed handler for `getAsync` will receive an `HttpResponseMessage` object, as we'll see in a moment.

**Handle exceptions!** It's very important with HTTP requests that you handle exceptions, that is, provide an error handler for methods like `getAsync`. Unhandled exceptions arising from HTTP requests have been found to be one of the leading causes of abrupt app termination!

For other HTTP operations, you can see in Figure 4-5 that we have `putAsync`, `postAsync`, and `deleteAsync`, along with the wholly generic `sendRequestAsync`. With the latter, its `message` argument is again an `HttpRequestMessage` as used with `getAsync`, only here you can also set the HTTP `method` that will be used (this is an `HttpMethod` object that also allows for additional options). `deleteAsync`, for its part, works completely from the URI parameters.

In the cases of put and post, the arguments to the methods are the URI and `content`, which is an object that provides the relevant data through methods and properties of the `HttpContent` interface (see the lower left of Figure 4-5). It's not expected that you create such objects from scratch (though you can)—WinRT provides built-in implementations called `HttpBufferContent`, `HttpStringContent`, `HttpStreamContent`, `HttpMultipartContent`, `HttpMultipartFormDataContent`, and `HttpFormUrlEncodedContent`.

What you then get back from `getAsync`, `sendRequestAsync`, and the delete, put, and post methods is an `HttpResponseMessage` object. Here you'll find all the bits you would expect:

- `statusCode`, `reasonPhrase`, and some helper methods for handling errors—namely, `EnsureSuccessStatusCode` (to throw an exception if a certain code is not received) and `isSuccessStatusCode` (to check for the range of 200–299).
- A collection of `headers` (of type `HttpResponseHeaderCollection`), which then leads to many other secondary classes.
- The original `requestMessage` (an `HttpRequestMessage`).
- The `source`, a value from `HttpResponseMessageSource` that tells you whether the data was received over the network or loaded from the cache.
- The response `content`, an object with the `HttpContent` interface as before. Through this you can obtain the response data as a string, buffer, input stream, and an in-memory array (`bufferAllAsync`).

<sup>37</sup> This read-only property works with certificates for SSL connections and contains the results of SSL negotiations; see `HttpTransportInformation`. To set a client certificate, there's a property on the `HttpBaseProtocolFilter`.

It's clear, then, that the HttpClient object really gives you complete control over whatever kind of HTTP requests you need to make to a service, including additional capabilities like cache control and cookie management as described in the following two sections. It's also clear that HttpClient is still somewhat of a low-level API. For any given web service that you'll be working with, then, I very much recommend creating a layer or library that encapsulates requests to that API and the process of converting responses into the data that the rest of the app wants to work with. This way you can also isolate the rest of the app from the details of your backend, allowing that backend to change as necessary without breaking the app. It's also helpful if you want to incorporate additional features of the Windows.Web.Http API, such as filtering, cache control, and cookie management.

I'd love to talk about cookies first (it's always nice to eat dessert before the main meal) but it's all part of filtering. Filtering is a mechanism through which you can control how the HttpClient manages its requests and responses. A filter is either an instance of the default HttpBaseProtocolFilter class (in the Windows.Web.Http.Filters namespace) configured for your needs or an instance of a derived class. You pass this filter object to the HttpClient constructor, which will use HttpBaseProtocolFilter as a default if none is supplied. To do things like cache control, though, you create an instance of HttpBaseProtocolFilter directly, set properties, and then create the HttpClient with it.

Tip It's perfectly allowable and encouraged, even, to create multiple instances of HttpClient when you need different filters and configurations for different services. There is no penalty in doing so, and it can greatly simplify your programming model.

The filter is essentially a black box that takes an HTTP request and produces an HTTP response—refer to Figure 4-5 again for its place in the whole process. Within the filter you can handle details like credentials, proxies, certificates, and redirects, as well as implement retry mechanisms, caching, logging, and so forth. This keeps all those details in a central place underneath the HttpClient APIs such that you don't have to bother with them in the code surrounding HttpClient calls.

With cache control, a filter contains a cacheControl property that can be set to an instance of the HttpCacheControl class. This object has two properties, readBehavior and writeBehavior, which determine how caching is applied to requests going through this filter. For reading, readBehavior is set to a value from the HttpCacheReadBehavior enumeration: default (works like a web browser), mostRecent (does an if-modified-since exchange with the server), and onlyFromCache (for offline use). For writing, writeBehavior can be a value from HttpCacheWriteBehavior, which supports default and noCache.

Managing cookies happens on the level of the filter as well. By default—through the HttpBaseProtocolFilter—the HttpClient automatically reads incoming set-cookie headers, saves the resulting cookies as needed, and then adds cookies to outgoing headers as appropriate. To access these cookies, create the HttpClient with an instance of HttpBaseProtocolFilter. Then you can access the filter's cookieManager property (that sounds like a nice job). This property is an instance of HttpCookieManager and has three methods: getCookies, setCookie, and deleteCookie. These allow you to examine specific cookies to be sent for a request or to delete specific cookies for privacy concerns.

Cookie behavior in general follows the same patterns as the browser. A cookie will persist across app sessions depending on the normal cookie rules: the cookie must be marked as persistent, is subject to the normal per-app limitations, and so on. Also note that cookies are isolated between apps for normal security reasons, even if those apps are using the same online resource.

For additional thoughts on HttpClient, refer to Updating Your JavaScript Apps to Use the New Windows Web HTTP API on the Windows App Builder blog. Demonstrations of the API, including filtering, can then be found in the HttpClient sample in the Windows SDK. Here's a quick run-down of what its scenarios demonstrate:

- **Scenarios 1–3** GET requests for text (with cache control), stream, and an XML list.
- **Scenarios 4–7** POST requests for text, stream, multipart MIME form, and a stream with progress.
- **Scenarios 8–10** Getting, setting, and deleting cookies.
- **Scenario 11** A metered connection filter that implements cost awareness on the level of the filter.
- **Scenario 12** A retry filter that automatically handles 503 errors with Reply-After headers.

To run this sample you must first set up a localhost server along with a data file and an upload target page. To do this, make sure you have Internet Information Services installed on your machine, as described below in “Sidebar: Using the Localhost.” Then, from an administrator command prompt, navigate to the sample's Server folder and run the command powershell -file setupserver.ps1. This will install the necessary server-side files for the sample on the localhost (c:\inetpub\wwwroot).

## Sidebar: Using the Localhost

The localhost is a server process that runs on your local machine, making it possible to debug both sides of client-server interactions. For this you can use a server like Apache or you can use the solution that's built into Windows and integrated with the Visual Studio tools: Internet Information Services (IIS).

To turn on IIS in Windows, go to Control Panel > Programs and Features > Turn Windows Features On or Off. Check the Internet Information Services box at the top level, as shown below, to install the core features:
