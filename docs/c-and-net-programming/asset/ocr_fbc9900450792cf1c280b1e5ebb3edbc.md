# File Version

The assembly file version attribute should be incremented automatically when the build is performed. In the beginning of the build process, Build number portion of the file version is incremented before the build label is applied to source control. It is displayed by windows explorer and never used by .Net framework for referencing.

# Assembly Version

The assembly version is used by .Net when linking assemblies. Assembly versions are incremented manually when code branching is done for a release. This should be specified in a "shared assembly info" that ensures that all of the various assemblies in the solution have the same assembly versions. CLR looks for this version no at runtime.

# Web API Versioning

Web API Versioning is required as the site size (in terms of coding) grows and business requirement changes with the time. As Web API can be consumed by multiple clients at a time, Versioning of Web API will be necessarily required so that Business changes in the API will not impact the client that are using/consuming the existing API.

Web API Versioning can be done by using the following methods,

+   1. URI
+   2. QueryString parameter
+   3. Custom Header parameter
+   4. Accept Header parameter

+   1. **Web API Versioning using URI :** In this method, Web API URI is changed with the help of routing and is more readable. Suppose there is an existing running API in which one URI returns some response. All Clients are consuming the same API and one client wants some changes by requesting to add new properties. With Versioning, one can achieve the same without breaking the existing API flow. In this case, Web API Versioning using URI is one of the best ways to achieve the same.
+   2. **Web API Versioning using QueryString parameter :** In Web API Versioning using Query String, a query string parameter is added to the query string in order to find the controller or Action to which request is sent. Whenever a request comes, SelectController() method of DefaultHttpControllerSelector Class selects the controller information from the information passed in the URI. In order to achieve the versioning with Query String, we need to create a Custom DefaultHttpControllerSelector and override the SelectController() method.