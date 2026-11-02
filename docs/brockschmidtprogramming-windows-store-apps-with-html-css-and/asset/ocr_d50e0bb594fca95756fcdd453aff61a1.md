Cookie behavior in general follows the same patterns as the browser. A cookie will persist across app sessions depending on the normal cookie rules: the cookie must be marked as persistent, is subject to the normal per-app limitations, and so on. Also note that cookies are isolated between apps for normal security reasons, even if those apps are using the same online resource.

For additional thoughts on HttpClient, refer to Updating Your JavaScript Apps to Use the New Windows Web HTTP API on the Windows App Builder blog. Demonstrations of the API, including filtering, can then be found in the HttpClient sample in the Windows SDK. Here's a quick run-down of what its scenarios demonstrate:

+   - **Scenarios 1–3** GET requests for text (with cache control), stream, and an XML list.
+   - **Scenarios 4–7** POST requests for text, stream, multipart MIME form, and a stream with progress.
+   - **Scenarios 8–10** Getting, setting, and deleting cookies.
+   - **Scenario 11** A metered connection filter that implements cost awareness on the level of the filter.
+   - **Scenario 12** A retry filter that automatically handles 503 errors with Reply-After headers.

To run this sample you must first set up a localhost server along with a data file and an upload target page. To do this, make sure you have Internet Information Services installed on your machine, as described below in “Sidebar: Using the Localhost.” Then, from an administrator command prompt, navigate to the sample's Server folder and run the command powershell -file setupserver.ps1. This will install the necessary server-side files for the sample on the localhost (c:\inetpub\wwwroot).

# Sidebar: Using the Localhost

The localhost is a server process that runs on your local machine, making it possible to debug both sides of client's-server interactions. For this you can use a server like Apache or you can use the solution that's built into Windows and integrated with the Visual Studio tools: Internet Information Services (IIS).

To turn on IIS in Windows, go to Control Panel > Programs and Features > Turn Windows Features On or Off. Check the Internet Information Services box at the top level, as shown below, to install the core features: