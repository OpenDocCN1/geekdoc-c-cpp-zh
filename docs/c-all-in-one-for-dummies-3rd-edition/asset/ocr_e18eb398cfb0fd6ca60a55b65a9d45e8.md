So how does the member function know which instance to work with? A secret parameter gets passed into the member function: the `this` pointer. Suppose you have a class called `Gobstopper` that has a member function called `Chew()`. Next, you have an instance called `MyGum`, and you call the `Chew()` function like so:

```
~~~cpp
MyGum.Chew();
~~~
```

When the compiler generates assembly code for this, it actually passes a parameter into the function — the address of the `MyGum` instance, also known as the `this` pointer. Therefore only one `Chew()` function is in the code, but to call it you must use a particular instance of the class.

Because only one copy of the `Chew()` function is in memory, you can take its address. But to do so requires some sort of cryptic-looking code. Here it is, quick and to the point. Suppose your class looks like this:

```
~~~cpp
class Gobstopper {
public:
    int WhichGobstopper;
    int Chew(string name) {
        cout << WhichGobstopper << endl;
        cout << name << endl;
        return WhichGobstopper;
    }
};
~~~
```

The `Chew()` function takes a string and returns an integer. Here's a typedef for a pointer to the `Chew()` function:

```
~~~cpp
typedef int (Gobstopper::*GobMember)(string);
~~~
```

And here's a variable of the type `GobMember`:

```
~~~cpp
GobMember func = &Gobstopper::Chew;
~~~
```

If you look closely at the typedef, it looks similar to a regular function pointer. The only difference is that the classname and two colons precede the asterisk. Other than that, it's a regular old function pointer.

But whereas a regular function pointer is limited to pointing to functions of a particular set of parameter types and a return type, this function pointer shares those restrictions but has a further limitation: It can only point to member functions within the class `Gobstopper`.

To call the function stored in the pointer, you need to have a particular instance. Notice that in the assignment of `func` in the earlier code there was no instance, just the classname and function, `&Gobstopper::Chew`. So to call the function,