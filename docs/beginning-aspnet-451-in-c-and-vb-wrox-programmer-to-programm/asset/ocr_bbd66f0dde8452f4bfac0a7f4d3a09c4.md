| ATTRIBUTE | DESCRIPTION |
|---|---|
| localOnly | Specifies whether the special Trace.axd handler is accessible from the local host only. From a security point of view, you're best off to leave this set to true, which means the trace is not available to outside users. |
| mostRecent | Determines whether old trace records are discarded when the number of trace requests hits the requestLimit. When set to false, tracing is disabled automatically when the requestLimit is hit. |

When you have enabled tracing, you have two ways to read the trace information. When you have set pageOutput to true, the trace information is appended to each page, similar to what you saw with page-level tracing.

However, to make tracing less obtrusive, you can disable pageOutput and then request tracing information using a special file called Trace.axd. This is a virtual file, which means you won't find it in your website when you go looking for it. However, the ASP.NET run time knows it should provide you with tracing information when you request this special page. Although the file is virtual, you can still protect it using ASP.NET's URL security by adding a <location /> element to the main Web.config file as you've done with other file and folders.

You see how to enable tracing for the site in the following exercise.

# TRY IT OUT  Enabling Tracing for the Entire Site

In this Try It Out, you see how to enable site-wide tracing. First, you make a few changes to the Web.config file. You then browse your site, filling the trace log with your page requests. Finally, you request the special Trace.axd page to see the available trace log information.

+   1. Open Web.config and locate the opening <system.web> tag. As a direct child of that element, add the following configuration information to enable tracing:

```
<system.web>
    <trace mostRecent="true" enabled="true" requestLimit="100" pageOutput="false" localOnly="true" />
```

This enables the trace, but doesn't add its output to the page. Instead, you need to request the special Trace.axd page to see the trace information. Additionally, you make your system a little more secure by only allowing requests for the trace information from the local machine. Save and close Web.config.

2. Open the Target Browser drop-down on the Standard toolbar and select your preferred browser. Then right-click Default.aspx in the Solution Explorer and choose View in Browser.

3. Click around the site, opening pages, changing the theme, filling in the contact form, and so on.

4. After you have requested at least five pages, change the address bar of your browser as follows so it requests the special Trace.axd page:

```
http://localhost:49394/Trace.axd
```