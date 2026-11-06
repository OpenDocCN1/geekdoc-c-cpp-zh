# Listing 9-5 (continued)

```
```cpp
case '4':
    cout << "All I wanna know is WHY?" << endl;
    break;
case '5':
    cout << "Expensive but good taste you have!" << endl;
    break;
}

return 0;
}
```
```

# Supercharging enums with Classes

When you work with classes, you can use a technique called *wrapping*, which helps you manage a resource. In Book I, Chapter 8, we discuss the enum keyword and how you can use it to create your own types. However, when you print the enumeration, you don’t see the word, such as red or blue; you see a number. The `DisplayEnum` example, shown in Listing 9-6, is a simple class that *wraps* an enum type — essentially, it helps you convert the number into a human readable form, which is a kind of resource management. You can use this class with `enum ColorEnum`, as `main()` demonstrates. When you run this application, you see the single word red in the console.

# Listing 9-6: Creating a Class for enums

```
```cpp
#include <iostream>

using namespace std;

class Colors
{
public:
    enum ColorEnum {blue, red, green, yellow, black};
    Colors(Colors::ColorEnum value);
    string AsString();

protected:
    ColorEnum value;
};

Colors::Colors(Colors::ColorEnum intivalue)
{
    value = intivalue;
}

string Colors::AsString()
{
    switch (value)
    {
```
```