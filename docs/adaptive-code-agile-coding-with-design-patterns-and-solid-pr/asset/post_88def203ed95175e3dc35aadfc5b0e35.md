
Even with this change, the controller from the multiple implementation example is sufficient: it correctly asks for each interface as a separate constructor parameter. What needs to change is how you construct the controller and supply it with those parameters. This is shown in Listing 10-19.

## LISTING 10-19
Although it might look unusual, this is an expected side effect of interface segregation.

```csharp
public OrderController CreateSingleService()
{
    var crud = new CreateReadUpdateDelete<Order>();
    return new OrderController(crud, crud, crud);
}
```

First, you only need a single instance of the CreateReadUpdateDelete class. It implements all three interfaces, so it suffices for all three constructor parameters.

As unusual as that might look—passing in the same instance three times—it makes sense because each parameter requires a different facet of the class. This is a common side effect of the interface segregation principle.

Of the two variations explored, this single implementation for a suite of related—but segregated—interfaces is not as versatile as having multiple implementations. It is most commonly used for the leaf implementation of the interfaces—that is, the implementation that is neither decorator nor adapter. It is the one that does the actual work. The reason for this is that the context is the same across all implementations. Whether you are using NHibernate, ADO.NET, Entity Framework, or some other persistence framework, the leaf implementation is the one that directly uses these libraries. In each case—reading, saving, or deleting—that same library will be used to do the main work.

Some decorators and adapters also apply to the full suite of segregated interfaces, but it is more common for these to be implemented individually only on the appropriate interface.

## The Interface Soup anti-pattern

A common mistake is to take the segregated interfaces and reunify them in an aggregate interface for some reason, as Listing 10-20 demonstrates. This is usually done to avoid the odd-looking multiple injection shown earlier.

### LISTING 10-20
Interface segregation is wrongly circumvented when all interfaces are thrown together to form a soup.

```csharp
interface IInterfaceSoupAntiPattern<TEntity> : IRead<TEntity>, ISave<TEntity>, IDelete<TEntity>
{
}
```

This creates an “interface soup” that is made from constituent interfaces but undermines the benefits of interface segregation. Implementers will again be required to provide implementations of all operations, so there is no scope for targeted decoration.

## Splitting interfaces

The ability—or requirement—to decorate interfaces is only one reason that you might want to split a large interface into smaller constituents. However, I view this as a good enough reason for the practice.

Two more utilitarian reasons for interface segregation are based on client need and architectural design.

### Client need

Different developers work on different parts of code. Therefore, it is likely that two or more developers will converge at some point, with one using the interface of another. Having detailed, step-by-step instructions for an interface is not only unlikely, but also impractical. Writing any code—especially code that is sufficiently unit tested—takes time. Writing extensive documentation is tedious and time consuming. Instead, it is better to program as defensively as is possible, to prevent other developers—or even yourself in the future—from inadvertently doing something they shouldn’t with your interface.

It helps to remember that clients need only what they need. Monolithic interfaces tend to hand too much control to clients. Interfaces with many members allow clients to do more than they perhaps should, clouding the intent and misdirecting the focus.

### Functionality

Listing 10-21 shows an interface that allows clients to interact with a user’s settings—specifically, the user interface theme that the clients have set for the application. This example is surprising—it is an interface with a single property that, in this scenario, is still exposing too much to its client. How can you possibly segregate this further?

### LISTING 10-21
The user settings interface allows access to the application’s current theme.

```csharp
public interface IUserSettings
{
    string Theme
    {
        get;
        set;
    }
}
```

First, see the implementation in Listing 10-22, which uses the ConfigurationManager class to read and write to the AppSettings section of the configuration files.

### LISTING 10-22
An implementation that loads settings from the configuration file.

```csharp
public class UserSettingsConfig : IUserSettings
{
    private const string ThemeSetting = "Theme";

    private readonly Configuration config;

    public UserSettingsConfig()
    {
        config = ConfigurationManager.OpenExeConfiguration(ConfigurationUserLevel.None);
    }
    public string Theme
    {
        get
        {
            return config.AppSettings.Settings[ThemeSetting].Value;
        }
        set
        {
            config.AppSettings.Settings[ThemeSetting].Value = value;
            config.Save();
            ConfigurationManager.RefreshSection("appSettings");
        }
    }
}
```

So far, so what? Well, there are two clients to this interface. One is focused only on reading the data, and the other is focused on writing the data. Herein lies the problem, as shown in Listing 10-23.

### LISTING 10-23
The clients of the interface use the property for different purposes.

```csharp
public class ReadingController
{
    private readonly IUserSettings settings;

    public ReadingController(IUserSettings settings)
    {
        this.settings = settings;
    }

    public string GetTheme()
    {
        return settings.Theme;
    }
}
```

```csharp
// . . .
public class WritingController
{
    private readonly IUserSettings settings;

    public WritingController(IUserSettings settings)
    {
        this.settings = settings;
    }

    public void SetTheme(string theme)
    {
        settings.Theme = theme;
    }
}
```

As is to be expected, the ReadingController only uses the getter of the Theme property, whereas the WritingController only uses the setter of the Theme property. However, due to a lack of segregation, there is nothing to stop the writer from retrieving the theme, nor—which is more problematic—the reader from modifying the theme.

To be truly defensive and eliminate the possibility of interface misuse, you can segregate the read and write portions of the interface, as shown in Listing 10-24.

### LISTING 10-24
The interface is split into two parts: one for reading the theme, and one for writing it.

```csharp
public interface IUserSettingsReader
{
    string Theme
    {
        get;
    }
}
// . . .
public interface IUserSettingsWriter
{
    string Theme
    {
        set;
    }
}
```

Although this might look a little odd, it is valid C#. It is perhaps not unusual that an interface can dictate that implementers only supply a getter for a property, but it is slightly more unusual that it requires only a setter.

Each controller is now able to depend only on the interface that it truly requires. As Listing 10-25 shows, the ReadingController is paired with the IUserSettingsReader, and the WritingController is paired with the IUserSettingsWriter.

### LISTING 10-25
Each of the two controllers now depends only on the interface that it requires.

```csharp
public class ReadingController
{
    private readonly IUserSettingsReader settings;

    public ReadingController(IUserSettingsReader settings)
    {
        this.settings = settings;
    }

    public string GetTheme()
    {
        return settings.Theme;
    }
}
// ...
public class WritingController
{
    private readonly IUserSettingsWriter settings;

    public WritingController(IUserSettingsWriter settings)
    {
        this.settings = settings;
    }

    public void SetTheme(string theme)
    {
        settings.Theme = theme;
    }
}
```

Via interface segregation, you have prevented the reader from being able to write the user settings, and you have prevented the writer from being able to read the user settings. Developers are thus not able to accidentally dilute the purpose of the controller by mistakenly performing an operation that they should not.

The implementing class, which uses the ConfigurationManager, changes only very subtly, as shown in Listing 10-26.

### LISTING 10-26
The UsersSettingsConfig class now implements both interfaces, but clients are unaware.

```csharp
public class UserSettingsConfig : IUserSettingsReader, IUserSettingsWriter
{
    private const string ThemeSetting = "Theme";

    private readonly Configuration config;
```
