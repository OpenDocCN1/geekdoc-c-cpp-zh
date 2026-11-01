```
char askYesNo1()
{
    char response1;
    do
    {
        cout << "Please enter 'y' or 'n': ";
        cin >> response1;
    } while (response1 != 'y' && response1 != 'n');

    return response1;
}
```

```
char askYesNo2(string question)
{
    char response2;
    do
    {
        cout << question << " (y/n): ";
        cin >> response2;
    } while (response2 != 'y' && response2 != 'n');

    return response2;
}
```

# Returning a Value

You can return a value from a function to send information back to the calling code. To return a value, you need to specify a return type and then return a value of that type from the function.

# Specifying a Return Type

The first function I declare, askYesNo1(), returns a char value. You can tell this from the function prototype before main():

```
char askYesNo1();
```

You can also see this from the function definition after main():

```
char askYesNo1()
```