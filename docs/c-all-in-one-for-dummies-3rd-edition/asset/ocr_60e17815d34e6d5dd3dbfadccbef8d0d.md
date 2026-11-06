The following lines of code from the `Singleton` example show how to create such a class:

```
```cpp
class Planet
{
private:
    static Planet *inst;
    Planet() { }

public:
    static Planet *GetInstance();
};

Planet *Planet::inst = 0;

Planet *Planet::GetInstance()
{
    if (inst == 0)
    {
        inst = new Planet();
    }
    return inst;
}
```
```

To use this class, you do not just create an instance directly. Instead, you call the `GetInstance()` member function:

```
```cpp
Planet *MyPlanet = Planet::GetInstance();
```
```

You call this any time you want to get a copy of the single instance.

![](bbox=[0.144, 0.547, 0.23, 0.616])

Every time you call `GetInstance()`, you always get a pointer to the same instance.

Now take a look at the constructor. It's private. Therefore, if you attempt something like this somewhere outside the class (such as in `main()`)

```
```cpp
Planet MyPlanet;
```
```

you get a compiler error. In Code::Blocks, we get this error:

```
```text
error: 'Planet::Planet()' is private
error: within this context
```
```

Or if you try to create a pointer, you get the same error when you call `new`:

```
```cpp
Planet *MyPlanet = new Planet();
```
```

When you have a class such as this, you probably also want to ensure that nobody attempts to delete the single instance. Just as you would make the constructor private, you would also make the destructor private, as in this example:

```
```cpp
class Planet
{
private:
```
```