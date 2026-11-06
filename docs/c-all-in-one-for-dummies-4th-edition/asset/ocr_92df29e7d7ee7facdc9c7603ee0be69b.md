# **LISTING 1-12:** *(continued)*

```
```cpp
void WhatIsMyName();
};

Squirrel::Squirrel(string StartName) {
    cout << "Starting!" << endl;
    Name = StartName;
}

void Squirrel::WhatIsMyName() {
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

In `main()`, you pass a string into the constructors. The constructor code takes the `StartName` parameter and copies it to the `Name` property. The `WhatIsMyName()` method writes `Name` to the console.

# # Building Hierarchies of Classes

When you start going crazy describing classes, you usually discover *hierarchies* of classes. For example, you have a class `Vehicle` that you want to divide into classes: `Car`, `PickupTruck`, `TractorTrailer`, and `SUV`. The `Car` class is further divided into the `StationWagon`, `FourDoorSedan`, and `TwoDoorHatchback` classes.