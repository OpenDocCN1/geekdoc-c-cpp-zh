The catch statement is catching a reference. Normally you can have references only to variables, not to values! But it works here because inside the computer, the application makes a temporary variable, and that’s what you’re referring to in the catch block. So all is fine.

# Catching any exception

If you want to write a general catch handler that will catch any exception and you don’t care to actually catch the object that was thrown, you can write your handler like this:

```
```cpp
try
{
    ProcessData();
    ProcessMore();
    cout << "No problems!" << endl;
}
catch (...)
{
    cout << "An unknown exception occurred." << endl;
}
```
```

That is, instead of putting what is effectively a function parameter in the catch header, you just put three dots, called an ellipsis.

![](bbox=[0.143, 0.51, 0.23, 0.58])

Some word processors (Microsoft Word being one) can transform three typed periods into a single ellipses character. Don’t paste that character into the code editor because the compiler won’t know what to do with it. Instead, type three periods.

You can use the ellipses also as a general exception catcher in addition to your other handlers. Here’s an example:

```
```cpp
try
{
    ProcessData();
    ProcessMore();
    cout << "No problems!" << endl;
}
catch (string excep)
{
    cout << "Found an error. Here's the message:";
    cout << endl;
    cout << excep;
    cout << endl;
}
catch (int num)
{
    cout << "Found a numerical error. Here it is.";
    cout << endl;
    cout << num;
    cout << endl;
}
```
```