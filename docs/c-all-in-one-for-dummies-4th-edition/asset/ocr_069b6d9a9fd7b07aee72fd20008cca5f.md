So how does the method know which instance to work with? The `this` parameter gets passed into the method to differentiate between instances. Suppose you have a class called Gobstopper that has a method called `Chew()`. Next, you have an instance called MyGum, and you call the `Chew()` method, like so:

```
```cpp
MyGum.Chew();
```
```

When the compiler generates assembly code for this, it actually passes a parameter into the function — the address of the MyGum instance, also known as the `this` pointer. Therefore only one `Chew()` function is in the code, but to call it, you must use a particular instance of the class.

Because only one copy of the `Chew()` method is in memory, you can take its address. But to do so requires some sort of cryptic-looking code. Here it is, quick and to the point. Suppose your class looks like this:

```
```cpp
class Gobstopper {
public:
    int WhichGobstopper;
    int Chew(string name) {
        cout << WhichGobstopper << endl;
        cout << name << endl;
        return WhichGobstopper;
    }
};
```
```

The `Chew()` method takes a string and returns an integer. Here’s a typedef for a pointer to the `Chew()` function:

```
```cpp
typedef int (Gobstopper::*GobMember)(string);
```
```

And here’s a variable of the type `GobMember`:

```
```cpp
GobMember func = &Gobstopper::Chew;
```
```

As with other functions, you can use `auto` to make things simple when you work with C++11 or above. Here’s the `auto` form of a variable that points to the `Chew()` method:

```
```cpp
auto func = &Gobstopper::Chew;
```
```

If you look closely at the typedef, it looks similar to a regular function pointer. The only difference is that the class name and two colons precede the asterisk. Other than that, it’s a regular old function pointer.

![](bbox=[0.17, 0.72, 0.24, 0.79])