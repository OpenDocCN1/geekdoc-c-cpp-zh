+   - protected
+   - private

These access specifiers denote the level of accessibility that the member has. In **SampleClass\Vehicle.h**, you can see two examples of how these are used. Note that unlike in C#, you do not restate the access specifier in front of each member. Instead, you state the access specifier, followed by a colon (e.g., `public:`), and then every declaration and definition that comes after is given that level of accessibility until you reach another access specifier.

By default, class members are private. This means if you have no access specifier at the beginning of the class declaration, then all members that are declared will be private until an access specifier is reached. If none is reached, you'd have an entirely private class, which would be very odd.

Structure members default to public, so on occasion you'll see a structure without any access specifiers. If you wish to use them in a structure, though, they work the same as in a class.

Lastly, you can use the same access specifier more than once; if you want to organize your class so you define the member functions first and then the member variables (or vice versa), you could easily do something like this:

*Note: This code is expository only; it is not included in any of the samples.*

```
```cpp
#include <string>

class SomeClass
{
public:
    SomeClass(void);
    virtual ~SomeClass(void);
    int AddTwoInts(int, int);
    void StoreAString(const wchar_t*);

private:
    bool CheckForIntAdditionOverflow(int, int);

public:
    int SomePublicInteger;

protected:
    std::wstring m_storedString;
};
```
```

The previous class definition doesn't define anything particularly useful. However, it does serve as an example of the use of all three access specifiers. It also demonstrates that you can use specifiers more than once, such as public in the previous example.

# # Inheritance

When specifying classes that your class derives from in C++, you should also specify an access specifier. If not, you will get the default access levels: private for a class and public for a structure. Note that I said classes. C++ supports multiple-inheritance. This means a class or structure can have more than one direct base class or structure, unlike C# where a class can have only one parent.