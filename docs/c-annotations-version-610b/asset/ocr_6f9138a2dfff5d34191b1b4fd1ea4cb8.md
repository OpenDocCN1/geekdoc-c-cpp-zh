```
```cpp
void Thrower::intThrower(int x) const throw(int)
{
    if (x)
        throw x;
}

void charPintThrower() throw(char const *, int)
{
    int x;

    cerr << "Enter an int: ";
    cin >> x;

    Thrower().intThrower(x);
    throw "this text is thrown if 0 was entered";
}

void runTimeError() throw(int)
{
    throw 12.5;
}

int main()
{
    try
    {
        charPintThrower();
    }
    catch (char const *message)
    {
        cerr << "Text exception: " << message << '\n';
    }
    catch (int value)
    {
        cerr << "Int exception: " << value << '\n';
    }
    try
    {
        cerr << "Generating a run-time error\n";
        runTimeError();
    }
    catch(...)
    {
        cerr << "not reached\n";
    }
}
```
```

A function without a throw list may throw any kind of exception. Without a function throw list the program's designer is responsible for providing the correct handlers.

For various reason declaring exception throwers is a questionable activity. Declaring exception throwers does not imply that the *compiler* checks whether an improper exception is thrown. Rather, the function will be surrounded by additional code in which the actual exception that is thrown is processed. Instead of compile time checks one gets run-time overhead, resulting in additional code (and execution time) that is added to the function's code. One could write, e.g.,

```
```cpp
void fun() throw (int)
{
```
```