

首先，查看清单 8-22 中的实现，它使用 ConfigurationManager 类来读取和写入配置文件中 AppSettings 部分的数据。

## LISTING 8-22 An implementation that loads settings from the configuration file.

Click here to view code image

```
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

到目前为止，有什么意义呢？好吧，这个接口有两个客户端。一个只关注读取数据，另一个只关注写入数据。问题就在于此，如清单 8-23 所示。

## LISTING 8-23 The clients of the interface use the property for different purposes.

Click here to view code image

```
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
//...
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

不出所料，ReadingController 只使用 Theme 属性的 getter，而 WritingController 只使用 Theme 属性的 setter。然而，由于缺乏隔离，无法阻止写入者检索主题，也无法阻止——更成问题的是——读取者修改主题。

为了真正做到防御性并消除接口误用的可能性，你可以对接口的读写部分进行分离，如清单 8-24 所示。

## LISTING 8-24 The interface is split into two parts: one for reading the theme, and one for writing it.

Click here to view code image

```
public interface IUserSettingsReader
{
    string Theme
    {
        get;
    }
}
//...
public interface IUserSettingsWriter
{
    string Theme
    {
        set;
    }
}
```

虽然这看起来有点奇怪，但它是完全有效的 C#。接口可以规定实现者仅提供属性的 getter，这或许并不罕见，但要求仅提供 setter 则稍显不寻常。

每个控制器现在都只能依赖于它真正需要的接口。如清单 8-25 所示，ReadingController 与 IUserSettingsReader 配对，而 WritingController 与 IUserSettingsWriter 配对。

## LISTING 8-25 Each of the two controllers now depends only on the interface that it requires.

Click here to view code image

```
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
//...
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

通过接口隔离，你阻止了读取者写入用户设置，也阻止了写入者读取用户设置。开发者因此无法因错误执行不应执行的操作而意外稀释控制器的目的。

实现类，即使用 ConfigurationManager 的类，仅做了非常细微的更改，如清单 8-26 所示。

## LISTING 8-26 The UsersSettingsConfig class now implements both interfaces, but clients are unaware.

Click here to view code image

```
public class UserSettingsConfig : IUserSettingsReader, IUserSettingsWriter
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

除了继承自读写两个接口之外，这个类与之前的版本完全相同。记住，同样的实现可以轻松地传递给 ReadingController 和 WritingController，但接口提供的窗口意味着 get 和 set 操作分别将不可用。

某些客户端应能够读取但不能写入的要求尤其常见。另一种情况，即不允许写入者读取，则不太可能。在这种情况下，你可以进行分离并继承接口，如清单 8-27 所示。

## LISTING 8-27 Now using methods, the writer inherits from the reader.

Click here to view code image

```
public interface IUserSettingsReader
{
    string GetTheme();
}
//...
public interface IUserSettingsWriter : IUserSettingsReader
{
    void SetTheme(string theme);
}
```

为了做到这一点，Theme 属性必须转换为 GetTheme 和 SetTheme 方法。这是因为语言并不完全干净地支持属性继承。Theme 属性同时存在于两个接口上。虽然类能够从两个不同的接口干净地实现 get 和 set 部分，但这在接口继承中却不幸不成立。当通过接口继承导致属性名称冲突时，编译器会警告基类属性被子类属性隐藏。这不会达到你想要的结果，而且编译器建议用 new 关键字替换基类属性也不是解决方案——getter 仍然不会被继承。

相反，你可以将属性更改为具有相同语义功能的方法。GetTheme 方法与 Theme.get 相同，SetTheme 方法与 Theme.set 相同。现在继承按预期工作——读取者接口的实现者和客户端将只能访问 GetTheme 方法，而写入者接口的实现者和客户端将同时访问 GetTheme 和 SetTheme 方法。此外，任何 IUserSettingsWriter 接口的实现自动也是 IUserSettingsReader 接口的实现。

清单 8-28 显示了对写入控制器的更改：它首先检查主题是否已更改，然后再尝试设置新主题。现在这是可以接受的，因为用户设置写入服务也是用户设置读取服务。在这种情况下，两个接口无需分别提供即可使用。

## LISTING 8-28 The writing controller has access to both the getter and setter through one interface.

Click here to view code image

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
        if(settings.GetTheme() != theme)
        {
            settings.SetTheme(theme);
        }
    }
}
```

## Authorization

按客户端需求进行分离的另一个例子是，当应用程序处于特定状态时才可用的一组操作。例如，用户可以执行的操作通常取决于该用户是否已登录。

清单 8-29 中显示的未授权接口包含匿名、未经身份验证的用户可以执行的操作。

## LISTING 8-29 This interface only contains operations that anonymous users can perform.

Click here to view code image

```
public interface IUnauthorized
{
    IAuthorized Login(string username, string password);

    void RequestPasswordReminder(string emailAddress);
}
```

请注意，Login 方法返回一个接口。只有在凭据正确时才会返回它，并且它允许客户端执行授权操作，如清单 8-30 所示。

## LISTING 8-30 After logging in, the user will have access to privileged operations.

