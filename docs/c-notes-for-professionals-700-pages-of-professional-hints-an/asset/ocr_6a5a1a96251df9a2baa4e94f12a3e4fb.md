Here is an example of the anti-pattern:

```
```
try
{
    while (AccountManager.HasMoreAccounts())
    {
        account = AccountManager.GetNextAccount();
        if (account.Name == userName)
        {
            //We found it
            throw new AccountFoundException(account);
        }
    }
}
catch (AccountFoundException found)
{
    Console.Write("Here are your account details: " + found.Account.Details.ToString());
}
```
```

Here is a better way to do it:

```
```
Account found = null;
while (AccountManager.HasMoreAccounts() && (found==null))
{
    account = AccountManager.GetNextAccount();
    if (account.Name == userName)
    {
        //We found it
        found = account;
    }
}
Console.Write("Here are your account details: " + found.Details.ToString());
```
```

catch (Exception)

There are almost no (some say none!) reasons to catch the generic exception type in your code. You should catch only the exception types you expect to happen, because you hide bugs in your code otherwise.

```
```
try
{
    var f = File.Open(myfile);
    // do something
}
catch (Exception x)
{
    // Assume file not found
    Console.Write("Could not open file");
    // but maybe the error was a NullReferenceException because of a bug in the file handling code?
}
```
```

Better do:

```
```
try
{
    var f = File.Open(myfile);
    // do something which should normally not throw exceptions
}
catch (IOException)
{
    Console.Write("File not found");
}
```
```