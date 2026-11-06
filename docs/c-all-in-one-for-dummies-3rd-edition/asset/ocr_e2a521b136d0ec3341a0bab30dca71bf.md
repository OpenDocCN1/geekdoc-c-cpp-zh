# ### Listing 8-11 (continued)

```
```cpp
void Squirrel::WhatIsMyName()
{
    cout << "My name is " << Name << endl;
}

int main()
{
    Squirrel *Sam = new Squirrel("Sam");
    Squirrel *Sally = new Squirrel("Sally");

    Sam->WhatIsMyName();
    Sally->WhatIsMyName();

    delete Sam;
    delete Sally;

    return 0;
}
```
```

In `main()`, we passed a string into the constructors. In the code for the constructor, we're taking the string parameter called `StartName` and copying it to the member variable called `Name`. In the `WhatIsMyName` function, we write it to the console.

![](bbox=[0.145, 0.475, 0.235, 0.555])

You cannot include parameters in a destructor. The C++ language does not allow it.

# ## Building Hierarchies of Classes

When you start going crazy describing classes, you usually discover *hierarchies of classes*. For example, you might say you have a class `Vehicle`. But we might say, we can divide your class `Vehicle` into classes `Car`, `Pickup Truck`, `Tractor Trailer`, and `SUV`.

Then you might say that you can take the `Car` class and divide it into such classes as `Station Wagon`, `Four-door Sedan`, and `Two-door Hatchback`.

Or we could divide `Vehicle` into car brands, such as `Ford`, `Honda`, and `Toyota`. Then we could divide the class `Toyota` into models, such as `Prius`, `Avalon`, `Camry`, and `Corolla`.

You can create similar groupings of objects for the other class hierarchies; your decision depends on how you categorize things and how the hierarchy is used.

In the hierarchy, class `Vehicle` is at the top. This class has characteristics that you find in every brand or model of vehicles. For example, all vehicles have wheels. How many they have varies, but it doesn't matter at this point because classes don't have specific values for the characteristics.