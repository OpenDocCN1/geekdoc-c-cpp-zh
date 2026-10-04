| maxInvalidPasswordAttempts | Specifies the number of times a user can enter an invalid password or invalid security answer before their account is locked. Defaults to 5. |
| minRequiredPasswordLength | Determines the minimum length of the password. Defaults to 7. |
| minRequiredNon alphanumericCharacters | Determines the minimum number of non-alphanumeric characters that must be included in the password. Defaults to 1. |
| passwordAttemptWindow | Determines the timeframe in minutes during which invalid password attempts are counted. Defaults to 10. |
| passwordStrengthRegularExpression | Enables you to specify a custom regular expression to enforce a strong password. |

Check out the complete list of configuration settings for Membership on the MSDN website at http://bit.ly/RFxQZT.

In the following Try It Out, you see what it takes to reconfigure the Membership provider for the Planet Wrox application by changing some of these attributes.

# TRY IT OUT Configuring Membership

In this short exercise, you see how to override the default behavior for the Membership provider in the Planet Wrox site to require users to enter a longer and stronger password.

+   1. Open Web.config and locate the <membership> element.
2. Change minRequiredPasswordLength to 7.
3. Change minRequiredNon alphanumericCharacters to 1. When you're done, your configuration settings should look like this:

```
<membership defaultProvider="DefaultMembershipProvider">
  <providers>
    <add name="DefaultMembershipProvider"
      type="System.Web.Providers.DefaultMembershipProvider,
      System.Web.Providers, Version=2.0.0.0, Culture=neutral,
      PublicKeyToken=31bf3856ad364e35"
      connectionStringName="PlanetWroxConnectionString1"
      enablePasswordRetrieval="false" enablePasswordReset="true"
      requiresQuestionAndAnswer="false" requiresUniqueEmail="false"
      maxInvalidPasswordAttempts="5" minRequiredPasswordLength="7"
      minRequiredNon alphanumericCharacters="1" passwordAttemptWindow="10"
      applicationName="/" />
  </providers>
</membership>
```