Write-only properties are useful for secure data such as passwords. Ideally, an application that implements security should allow you to set your password but never allow you to read it back. When a user attempts to log on, the user can provide the password. The logon method can compare this password with the stored password and return only an indication of whether they match.

# Property accessibility

You can specify the accessibility of a property using the keywords public, private, or protected when you declare it. However, it's possible within the property declaration to override the property accessibility for the get and set access. For example, the version of the ScreenPosition structure shown in the code that follows the set access of the x and y properties as private. (The get access are public because the properties are public.)

Click here to view code image

```
struct ScreenPosition
{
    private int _x, _y;
    ...
    public int X
    {
        get => this._x;
        private set => this._x = rangeCheckedX(value);
    }
    public int Y
    {
        get => this._y;
        private set => this._y = rangeCheckedY(value);
    }
    ...
}
```

You must observe some rules when defining accessors that have different accessibility from one another:

+   You can change the accessibility of only one of the accessors when you define it. It wouldn't make much sense to define a property as public only to change the accessibility of both access to private anyway.