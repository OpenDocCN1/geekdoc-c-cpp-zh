# Table 36.14: Noteworthy Properties of the FormsAuthentication Class

| Property | Description |
|---|---|
| CookiesSupported | Returns a value that indicates whether the application allows cookieless Forms authentication. |
| DefaultUrl | Returns the default URL, that is, the URL to which users are redirected in the absence of a redirect URL. |
| EnableCrossAppRedirects | Returns a value that indicates if authenticated users can be redirected to Web pages of other ASP.NET applications. |
| FormsCookieName | Returns the name of the authentication cookie. |
| FormsCookiePath | Returns the path of the authentication cookie. |
| LoginUrl | Returns the URL of the login page to which unauthenticated users are redirected. |
| RequireSSL | Returns a value that indicates whether an SSL connection is required to send the authentication cookie to the Web server. |
| SlidingExpiration | Returns a value that indicates whether to use sliding expiration for the authentication cookie. If sliding expiration is enabled and if another request is made after half of the timeout interval, then the expiration time of the authentication cookie is reset. |

Table 36.15 lists the noteworthy methods of the FormsAuthentication class:

# Table 36.15: Noteworthy Methods of the FormsAuthentication Class

| Method | Description |
|---|---|
| Authenticate() | Checks the authenticity of the credentials provided by the user against the credentials stored in a database or application |
| Decrypt() | Uses an encrypted Forms authentication ticket to create an authentication ticket |
| Encrypt() | Creates a string object to hold the encrypted Forms authentication ticket |
| GetAuthCookie() | Creates an authentication cookie for a particular user name |
| GetRedirectUrl() | Returns the URL of the original request that causes a redirect to the login page |
| HashPasswordForStoringInConfigFile() | Uses a given password and hash algorithm to generate a hash password that can be stored in a configuration file |
| Initialize() | Initializes a FormsAuthentication object |
| RedirectFromLoginPage() | Redirects an authenticated user back to the default or the originally requested URL |
| RedirectToLoginPage() | Redirects an unauthenticated user to the login page |
| RenewTicketIfOld() | Renews the authentication ticket by updating the date and time of issue of the ticket |
| SetAuthCookie() | Creates an authentication ticket for a particular user name and adds the ticket to the cookies collection or the URL. |
| SignOut() | Removes the authentication ticket from the authentication cookie or the URL |

# Passport Authentication

With the Passport authentication, you can use the single logon service provided by Microsoft for multiple websites. The Passport authentication provides a single centralized hub for authenticating users. The users simply need to provide the credentials on a login page and if authenticated, can use the services of other member sites without the need to login again on each site. To implement Passport authentication in ASP.NET applications, you need to first download the .NET Passport SDK from the .NET Passport/Microsoft website (www.microsoft.com). You then need to install the Passport SDK after which you can use the classes that allow you to implement Passport authentication.