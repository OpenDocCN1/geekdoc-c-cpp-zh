```
get
{
    return defaultInstance;
}
}
```

```
[global::System.Configuration.UserScopedSettingAttribute()]
[global::System.Diagnostics.DebuggerNonUserCodeAttribute()]
[global::System.Configuration.DefaultSettingValueAttribute("ftp://127.0.0.1")]
public string FTP_SERVER
{
    get
    {
        return ((string)(this["FTP_SERVER"]));
    }
    set
    {
        this["FTP_SERVER"] = value;
    }
}

[global::System.Configuration.UserScopedSettingAttribute()]
[global::System.Diagnostics.DebuggerNonUserCodeAttribute()]
[global::System.Configuration.DefaultSettingValueAttribute("anonymous")]
public string UserName
{
    get
    {
        return ((string)(this["UserName"]));
    }
    set
    {
        this["UserName"] = value;
    }
}

[global::System.Configuration.UserScopedSettingAttribute()]
[global::System.Diagnostics.DebuggerNonUserCodeAttribute()]
[global::System.Configuration.DefaultSettingValueAttribute("password")]
public string Password
{
    get
    {
        return ((string)(this["Password"]));
    }
    set
    {
        this["Password"] = value;
    }
}
```