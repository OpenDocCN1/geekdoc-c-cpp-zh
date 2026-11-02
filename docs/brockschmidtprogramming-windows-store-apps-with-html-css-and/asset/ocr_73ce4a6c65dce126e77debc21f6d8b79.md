the app, the app can talk directly with the service. Oftentimes a service will also provide for renewing the token as needed.

![](bbox=[0.15, 0.16, 0.88, 0.58])

FIGURE 4-8 The authentication flow with the web authentication broker.

In WinRT, the broker is represented by the Windows.Security.Authentication.Web.WebAuthenticationBroker class. Authentication happens through its authenticateAsync methods. I say "methods" here because there are two variations. We'll look at one here and return to the second in the next section, "Single Sign-On."

This first variant of authenticateAsync method takes three arguments:

+   - **options** Any combination of values from the webAuthenticationOptions enumeration (combined with bitwise OR). Values are none (the default), silentMode (no UI is shown), useTitle (returns the window title of the webpage in the results), useHttpPost (sends the authentication token through HTTP POST rather than on the URI, to accommodate long tokens that would make the URI exceed 2K), and useCorporateNetwork (to render the web page in an app container with the Private Networks (Client & Server), Enterprise Authentication, and Shared User Certificates capabilities; the app must have also declared these).
+   - **requestUri** The URI (Windows.Foundation.Uri) for the provider's authentication page along with the parameters required by the service; again, this must use the https:// URI scheme.
+   - **callbackUri** The URI (Windows.Foundation.Uri) of the provider's final page in its authentication process. The broker uses this to determine when to take down its UI.