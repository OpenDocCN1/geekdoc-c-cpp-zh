| Table 9.3: Attributes Supported by @ OutputCache Directive |  |
|---|---|
| **Attribute** | **Description** |
| CacheProfile | Contains the name of the cache settings associated with a Web page; this is an optional attribute and by default, it contains an empty string. |
| Duration | Defines the time duration in seconds for the Web page or the user control that is being cached. This attribute is required. |
| Location | Defines the location where cache is created. The possible values are Any, Client, Downstream, Server, and None. |
| NoStore | Contains a Boolean value that determines whether to prevent secondary storage of sensitive information or not. |
| Shared | Sets a Boolean value that allows you to share the output of cached control with multiple pages. |
| SqlDependency | Contains a string value, which identifies a set of database and table name pairs, on which the output cache of the Web page depends. |
| VaryByControl | Contains a semicolon-separated list of strings that is used to vary the output cache. These strings represent ID of the property value of the ASP.NET server controls on a user control; if you are working with user controls and not using the **VaryByParam** attribute, then the **VaryByControl** attribute is necessary (this attribute is not supported for ASP.NET Web pages). |
| VaryByCustom | Defines custom strings for the custom output caching requirements. |
| VaryByHeader | Defines a semicolon-separated list of HTTP headers, used to vary the output cache. |
| VaryByParam | Defines a semicolon-separated list of strings, used to vary the output cache. This attribute is required. |
| VaryByContentEncodings | Defines a semicolon-separated list of strings used to vary the output cache. This attribute is used by the Accept-Encoding header to determine how cached responses are served for different content encodings (changing the format of the content to some other format). |

Now, let’s discuss some important attributes of the **@ OutputCache** directive in detail.

# The Location Attribute

The **Location** attribute is used to define the location where the item needs to be cached. It can be on the server side or on the client side or can even be on the proxy server. The **Location** attribute takes its values from the **OutputCacheLocation** enumeration. All the possible values of the **OutputCacheLocation** enumeration are listed in Table 9.4:

| Table 9.4: Possible Values for the OutputCacheLocation Enumeration |  |
|---|---|
| **Value** | **Description** |
| Any | Specifies that the output cache can be stored anywhere, such as on the client browser, proxy server, or Web server itself |
| Client | Specifies that the output cache is only located on the client browser |
| Downstream | Specifies that the output cache can be stored in any of the HTTP 1.1 cache-capable devices, other than the originating server, which can be a proxy server or the client that made the request |
| None | Disables the output cache of the requested page |
| Server | Specifies that the output cache is only located on the Web server |
| ServerAndClient | Specifies that the output cache is stored on the Web server as well as on the client browser |