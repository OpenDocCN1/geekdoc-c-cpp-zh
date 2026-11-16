This code snippet configures Google and Facebook authentication, retrieving the necessary client IDs and secrets from your application's configuration.

+   3. **Add Login Buttons:** In your Razor views, add login buttons or links for each social login provider you support.

```
Razor CSHTML

<a asp-action="ExternalLogin" asp-route-provider="Google">Login with Google</a>
<a asp-action="ExternalLogin" asp-route-provider="Facebook">Login with Facebook</a>
```

These links trigger the ExternalLogin action method in your controller, passing the provider name as a route parameter.

+   4. **Handle External Login Callback:** Implement the ExternalLogin action method in your controller to initiate the authentication flow with the selected provider.

```
C#

[HttpPost]
[AllowAnonymous]
public IActionResult ExternalLogin(string provider, string returnUrl = null)
{
    var redirectUrl = Url.Action("ExternalLoginCallback", "Account", new
    {
        ReturnUrl = returnUrl
    });
    var
    properties =
    _signInManager.ConfigureExternalAuthenticationProperties(provider,
    redirectUrl);
    return new ChallengeResult(provider, properties);
}
```