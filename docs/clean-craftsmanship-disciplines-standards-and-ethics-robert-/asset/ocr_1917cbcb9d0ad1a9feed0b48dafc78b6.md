And let's say that the `DatabaseConnection` class has a constructor that requires valid `UID`s for a `databaseUser` and `databaseAuthCode`. (I'm sure you've seen situations like this.)

Click here to view code image

```
public class RealAuthenticator implements Authenticator {
    public RealAuthenticator(DatabaseConnection connection) {
        //...
    }

    //...

}
```

```
public class DatabaseConnection {
    public DatabaseConnection(UID databaseUser, UID databaseAuthCode)
{
        //...
    }
}
```

To use the `RealAuthenticator` in our test, we'd have to do something horrible, like this:

Click here to view code image

```
@Test
public void whenClosed_loginIsCancelled() throws Exception {
    UID dbUser = SecretCodes.databaseUserUID;
    UID dbAuth = SecretCodes.databaseAuthCode;
    DatabaseConnection connection =
        new DatabaseConnection(dbUser, dbAuth);
    Authenticator authenticator = new RealAuthenticator(connection);
    LoginDialog dialog = new LoginDialog(authenticator);
    dialog.show();
    boolean success = dialog.sendEvent(Event.CLOSE);
    assertTrue(success);
}
```

That's a terrible load of cruft to put into our test just so that we can create an `Authenticator` that will never be used. It also adds two dependencies to