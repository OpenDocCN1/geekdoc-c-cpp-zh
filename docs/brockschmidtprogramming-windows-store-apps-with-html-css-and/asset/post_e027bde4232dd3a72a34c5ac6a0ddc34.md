
```
https://www.facebook.com/dialog/oauth?client_id=<client_id>&redirect_uri=<redirectUri>&
scope=read_stream&display=popup&response_type=token
```

```
https://accounts.google.com/o/oauth2/auth?client_id=<client_id>&redirect_uri=<redirectUri>&
response_type=code&scope=http://picasaweb.google.com/data
```

where `<client_id>` and `<redirectUri>` are replaced with whatever is specific to the app. Twitter and Flickr, for their parts, use OAuth 1.0a protocol instead, so much more ceremony goes into creating the lengthy OAuth token to include with the `requestUri` argument to `authenticateAsync`. I’ll leave it to the sample code to show those details.

## Single Sign-On

What we’ve seen so far with the credential locker and the web authentication broker works very well to minimize how often the app needs to pester the user for credentials. Where a single app is concerned, it would ideally only ask for credentials once until such time as the user explicitly logs out. But what about multiple apps? Imagine over time that you acquire some dozens, or even hundreds, of apps from the Windows Store that use services that all require authentication. Even if those services exclusively use well-known OAuth providers, it’d still mean that you’d have to enter your Facebook, Twitter, Google, LinkedIn, Tumblr, Yahoo, or Yammer credentials in each and every app. At that point, the fact that you only need to authenticate each app once gets lost in the overall tedium!

From the user’s point of view, once they’ve authenticated through a given provider in one app, it makes sense that other apps should benefit from that authentication if possible. Yes, some apps might need to prompt for additional permissions and some providers may not support the process, but the ideal is again to minimize the fuss and bother where we can.

The concept of *single sign-on* is exactly this: authenticating the user in one app (or the system in the case of a Microsoft account) effectively logs the user in to other apps that use the same provider. To make this work, the web authentication broker keeps persisted logon cookies for each service in a special app container that’s completely isolated from apps but yet allows those cookies to be shared between apps (like cookies are shared between websites in a browser). At the same time, each app must often acquire its own access keys or tokens, because these should not be shared between apps. So the real trick is to effectively perform the same kind of authentication we’ve already seen, only to do it without showing any UI unless it’s really necessary.

This is the purpose of the variation of `authenticateAsync` that takes only the `options` and `requestUri` arguments (and not an explicit `callbackUri`). In this case `options` is often set to `WebAuthenticationOptions.silentMode` to prevent the broker’s UI from appearing (this isn’t required). But then how does the broker know when authentication is complete? That is, what `callbackUri` does it use for comparison, and how does the provider know that itself? It sounds like a situation where the broker would just sit there, forever hidden, while the provider patiently waits for input to a web page that’s equally invisible!

What actually happens is that `authenticateAsync` watches for the provider to navigate to a special `callbackUri` in the form of `ms-app://<SID>`, where `<SID>` is a security identifier that uniquely identifies the calling app. This SID URI, as we'll call it, is obtained in two ways. In code, call the static method `WebAuthenticationBroker.getCurrentApplicationCallbackUri`. This returns a `Windows.Foundation.Uri` object whose `absoluteUri` property is the string you need. The second means is through the Windows Store Dashboard. When viewing info for the app in question, go to the "Services" section. There you'll see a link to the "Live Services site" (rooted at https://account.live.com). On that site, click the link "Authenticating your service" and you'll see the URL listed here under Package Security Identifier (SID).

To understand how it's used, let's follow the entire flow of the silent authentication process:

- 1. The app registers its SID URI with the service. From code, this could be done through some service API or other endpoint that's been set up for this purpose. A service could have a page (like Facebook) where you, the developer, registers your app directly and provides the SID URI as part of the process.
- 2. When constructing the `requestUri` argument for `authenticateAsync`, the app inserts its SID URI as the value of the `&redirect_uri=` parameter. The SID URI will need to be appropriately encoded as other URI parameters, of course, using `encodeURIComponent`.
- 3. The app calls `authenticateAsync` with the `silentMode` option.
- 4. When the provider processes the `requestUri` parameters, it checks whether the `redirect_uri` value has been registered, responding with a failure if it hasn't.
- 5. Having validated the app, the provider then silently authenticates (if possible) and navigates to the `redirect_uri`, making sure to include things like access keys and tokens in the response data.
- 6. The web authentication broker will detect this navigation and match it to the app's SID URI. Finding a match, the broker can complete the async operation and provide the response data to the app.

With all of this, it's still possible that the authentication might fail for some other reason. For example, if the user has not set up permissions for the app in question (as with Facebook), it's not possible to silently authenticate. So, an app attempting to use single sign-on would call this form of `authenticateAsync` first and, failing that, would then revert to calling its longer form (with UI), as described in the previous section.

## Using the Microsoft Account

Because various Microsoft services are OAuth providers, it is possible to use the web authentication broker with a Microsoft account such as Hotmail, Live, and MSN. (I still have the same @msn.com email account [I've had since 1996!]) Details can be found on the OAuth 2.0 page on the Live Connect Developer Center.

Live Connect accounts—also known as Microsoft accounts—are in a somewhat more privileged position because they can also be used to sign in to Windows or can be connected to a domain account used for the same purpose. Many of the built-in apps such as Mail, Calendar, SkyDrive, People, and the Windows Store itself work with this same account. Thus, it's something that many other apps might want to take advantage of. Such apps automatically benefit from single sign-on and have access to the same Live Services that the built-in apps draw from themselves (including Skype, which has taken the place of Live Messenger).

The whole gamut of what's available can be found on the Live Connect documentation.46 You can access Live Connect features directly through its REST API as well as through the client side libraries of the Live SDK. When you install the SDK and add the appropriate references to your project, you'll have a WL namespace available in JavaScript. Signing in, for example, is accomplished through the WL.login method.

To explore Live Services a little, we'll first walk through the user experience that applies here and then we'll turn to the LiveConnect example in this chapter's companion content, which demonstrates using the Live SDK library. Note that when using Live Services, the app's package information in its manifest must match what exists in the Windows Store dashboard for your app. To ensure this, create the app profile in the dashboard (to what extent you can), go to Visual Studio, select the Store > Associate App with the Store menu command, sign in to the Store, and select your app.

## The OnlineId API in WinRT

The Windows.Security.Authentication.OnlineId namespace contains an API that has some redundancy with the Live SDK, providing another route to log in and obtain an access token. The Windows account authorization sample demonstrates this, using the token when making HTTP requests directly to the Live REST API. Although the sample includes a JavaScript version, the API is primarily meant for apps written in C++ where there isn't another option like the Live SDK. However, the API is also useful when the user logs into Windows with something other than a Microsoft account, such as a domain account. The OnlineIdAuthenticator.canSignOut property, for example, is set to true if the Microsoft account is not the primary login, and thus apps that use it should provide a means to sign out. The OnlineId API also provides for authenticating multiple accounts together (e.g., multiple SkyDrive accounts) and can work with provider like Windows Azure Active Directory and SkyDrive Pro.

## The Live Connect User Experience

Whenever an app attempts to log in to Live Connect for the first time, a consent dialog such as that in Figure 4-9 will automatically appear to make sure the user understands the kinds of information the app might access. If the user denies consent, then of course the login will fail. For this reason the app should provide a means through which the user can sign in again. (Also see Guidelines for the Microsoft account sign-in experience for additional requirements.)

46 Additional helpful references include Live Connect (Windows Store apps), Single sign-on for apps and websites, Using Live Connect to personalize apps, and Guidelines for the Microsoft account sign-in experience. Also see Bring single sign-on to your Windows apps with the Live SDK and Best practices when adding single sign-on to your app with the Live SDK on the Windows 8 Developer Blog (prior to the Windows App Builder blog).
