First, see the implementation in Listing 8-22, which uses the ConfigurationManager class to read and write to the AppSettings section of the configuration files.

# LISTING 8-22 An implementation that loads settings from the configuration file.

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

So far, so what? Well, there are two clients to this interface. One is focused only on reading the data and the other is focused on writing the data. Herein lies the problem, as shown in Listing 8-23.

# LISTING 8-23 The clients of the interface use the property for different purposes.

Click here to view code image

```
public class ReadingController
{
```