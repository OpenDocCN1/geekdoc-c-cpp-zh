```
public AccountBase CreateAccount(string accountType)
{
    var objectHandle = Activator.CreateInstance(null, string.Format("{0}Account", accountType));
    return (AccountBase)objectHandle.Unwrap();
}
```