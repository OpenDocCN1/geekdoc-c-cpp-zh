```
public interface IUserSettingsReader
{
    string GetTheme();
}
// ...
public interface IUserSettingsWriter : IUserSettingsReader
{
    void SetTheme(string theme);
}
```