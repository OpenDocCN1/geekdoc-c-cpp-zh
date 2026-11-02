Note that if you add a credential to the locker with a `resource` and `userName` that already exist, the new credential will replace the old. And if at any point you want to delete a credential from the locker, call the `PasswordVault.remove` method with that credential.

Furthermore, even though a `PasswordCredential` object sees the world in terms of usernames and passwords, that password can be anything you need to store securely, such as an access token. As we'll see in the next section, authentication through OAuth providers might return such a token, in which case you might store something like `"Facebook_Token"` in the credential's `resource` property, your app name in `userName`, and the token in `password`. This is a perfectly legitimate and expected use.

Once a credential is in the locker, it will remain there for subsequent launches of the app until you call the `remove` method or the user explicitly deletes it through Control Panel > User Accounts and Family Safety > Credential Manager. On a trusted PC (which requires sign-in with a Microsoft account), Windows will also automatically and securely roam the contents of the locker to the user's other devices (unless turned off in PC Settings > SkyDrive > Sync Settings > Other Settings > Passwords). This helps to create a seamless experience with your app as the user moves between devices.<sup>44</sup>

So, when you launch an app—even when launching it for the first time—always check if the locker contains saved credentials. There are several methods in the `PasswordVault` class for doing this:

+   - `findAllByResource` Returns an array (vector) of credential objects for a given resource identifier. This is how you can obtain the username and password that's been roamed from another device, because the app would have stored those credentials in the locker on the other machine under the same resource.
+   - `findAllByUserName` Returns an array (vector) of credential objects for a given username. This is useful if you know the username and want to retrieve all the credentials for multiple resources that the app connects to.
+   - `retrieve` Returns a single credential given a resource identifier and a username. Again, there will only ever be a single credential in the locker for any given resource and username.
+   - `retrieveAll` Returns a vector of all credentials in the locker for this app. The vector contains a snapshot of the locker and will not be updated with later changes to credentials in the locker.

There is one subtle difference between the `findAll` and `retrieve` methods in the list above. The `retrieve` method will provide you with fully populated credentials objects. The `findAll` methods, on the other hand, will give you objects in which the `password` properties are still empty. This avoids performing password decryption on what is potentially a large number of credentials. To populate that property for any individual credential, call the `PasswordCredential.retrievePassword` method.

For further demonstrations of the credential locker—the code is very straightforward—refer to the `Credential_locker sample`. This shows variations for single user/single resource (scenario 1), single

44 Such roaming will not happen, however, if a credential is *first* stored in the locker on a domain joined machine. This protects domain credentials from leaking to the cloud.