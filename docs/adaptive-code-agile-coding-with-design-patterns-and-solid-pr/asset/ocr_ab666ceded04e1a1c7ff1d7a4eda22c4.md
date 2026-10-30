Instead, you can change from properties to methods with the same semantic function. The GetTheme method is the same as Theme.get, and the SetTheme method is the same as Theme.set. Now inheritance works as expected—implementers and clients of the reader interface will only have access to the GetTheme method, and implementers and clients of the writer interface will have access to both the GetTheme and SetTheme methods. Additionally, any implementation of the IUser-SettingsWriter interface is also an implementation of the IUserSettingsReader interface.

Listing 10-28 shows a change to the writing controller: it first checks whether the theme has been changed before it tries to set a new theme. This is now acceptable because the user settings writer service is also the user settings reader service. In this case, the two interfaces do not need to be supplied separately to be used.

**LISTING 10-28** The writing controller has access to both the getter and setter through one interface.

```
public class WritingController
{
    private readonly IUserSettingsWriter settings;

    public WritingController(IUserSettingsWriter settings)
    {
        this.settings = settings;
    }

    public void SetTheme(string theme)
    {
        if (settings.GetTheme() != theme)
        {
            settings.SetTheme(theme);
        }
    }
}
```

# Authorization

Another example of segregation by client need is when a set of operations is only available when the application is in a specific state. For example, the operations that a user can perform are typically different depending on whether that user is logged in or not.

The IUnauthorized interface shown in Listing 10-29 contains operations that can be done by an anonymous, unauthenticated user.

**LISTING 10-29** This interface contains only operations that anonymous users can perform.

```
public interface IUnauthorized
{
    IAuthorized Login(string username, string password);

    void RequestPasswordReminder(string emailAddress);
}
```