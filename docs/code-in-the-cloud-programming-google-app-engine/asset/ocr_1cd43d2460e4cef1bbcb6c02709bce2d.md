that is accessible to every App Engine application, regardless of what framework you use for building your application. Even if you decide to use something like Django for your application, you can still use all of the App Engine services.

The easiest way to set up authentication is to use the Google App Engine users service to piggyback on Google accounts. If your application uses Google email addresses as its main identifier, then it can work with Google logins. You can build your own authentication service or use another third-party authentication service if you want; there’s nothing forcing you to use GAE’s login service. But it’s very convenient, and for most applications, it’s probably sufficient. Using other services won’t be very different—the basic mechanics will be similar.

# ## 5.2 The Users Service

Google logins are supported by the users service. The users service keeps track of a currently logged-in user and provides capabilities to allow your application to provide login and logout pages.

# ### User Objects and the Current User

The easiest thing to do with the users service is to retrieve the user object for the currently logged-in user. You can always retrieve the user by calling `users.get_current_user()`. If there’s no user logged in from that client, the call returns `None`. If there is a logged-in user, you get back a Python object with three instance methods:

+   - `nickname()` A textual name associated with the user. This will eventually be user configurable, but at the moment, it just returns the part of the email address before the @ symbol. In my case, it’s markcc.
+   - `email()` The user’s email address. In my case, it’s markcc@gmail.com.
+   - `user_id()` A permanent identifier for the user. Treat this as an opaque string. The users can change their email address or their nickname whenever they want, but their user_id will always be the same. This isn’t useful for display purposes, but if you want to record permanent information about a user—such as the set of orders placed by a user on a commerce site—you can use this as an identifier that will work no matter what.