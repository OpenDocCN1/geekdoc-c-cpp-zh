```
<add name="ClientRoleProvider"
type="System.Web.ClientServices.Providers.ClientRoleProvider,
System.Web.Extensions, Version=4.0.0.0, Culture=neutral,
PublicKeyToken=31bf3856ad364e35" serviceUrl="
http://localhost:55555/AppServices/Role_JSON_AppService.asmx"
cacheTimeout="86400" />
<providers>
<roleManager>
</system.web>
</configuration>
```

code snippet AuthenticationServices\app.config

The Windows application just uses Label, TextBox, PasswordBox, and Button controls, as shown in Figure 21-1. The Label with the content User Validated shows up only when the logon is successful.

The handler of the Button.Click event invokes the ValidateUser() method of the Membership class. Because of the configured provider ClientAuthenticationMembershipProvider, the provider in turn invokes the Web service and calls the method ValidateUser() of the SampleMembershipProvider class to verify a successful logon. With success, the Label labelValidatedInfo is made visible; otherwise, a message box pops up:

![](bbox=[0.62, 0.33, 0.85, 0.6])

FIGURE 21-1

```
private void OnLogin(object sender, RoutedEventArgs e)
{
    try
    {
        if (Membership.ValidateUser(textUsername.Text,
            textPassword.Password))
        {
            // user validated!
            labelValidatedInfo.Visibility = Visibility.Visible;
        }
        else
        {
            MessageBox.Show("Username or password not valid",
                "Client Authentication Services", MessageBoxButton.OK,
                MessageBoxImage.Warning);
        }
    }
    catch (WebException ex)
    {
        MessageBox.Show(ex.Message, "Client Application Services",
            MessageBoxButton.OK, MessageBoxImage.Error);
    }
}
```

code snippet AuthenticationServices/MainWindow.xaml.cs

# ENCRYPTION

Confidential data should be secured so that it cannot be read by unprivileged users. This is valid both for data that is sent across the network, or stored data. You can encrypt such data with symmetric or asymmetric encryption keys.

With a symmetric key, the same key can be used for encryption and decryption. With asymmetric encryption, different keys are used for encryption and decryption: a public and a private key. Something