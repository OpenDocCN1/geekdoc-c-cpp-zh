| Base-class access specifier | public inheritance | protected inheritance | private inheritance |
|---|---|---|---|
| public | public in derived class.<br><br>Can be accessed directly by member functions, friend functions and nonmember functions. | protected in derived class.<br><br>Can be accessed directly by member functions and friend functions. | private in derived class.<br><br>Can be accessed directly by member functions and friend functions. |
| protected | protected in derived class.<br><br>Can be accessed directly by member functions and friend functions. | protected in derived class.<br><br>Can be accessed directly by member functions and friend functions. | private in derived class.<br><br>Can be accessed directly by member functions and friend functions. |
| private | Inaccessible in the derived class.<br><br>Can be accessed by member functions and friend functions through public or protected member functions inherited from the base class. | Inaccessible in the derived class.<br><br>Can be accessed by member functions and friend functions through public or protected member functions inherited from the base class. | Inaccessible in the derived class.<br><br>Can be accessed by member functions and friend functions through public or protected member functions inherited from the base class. |

With public inheritance

+   - public base-class members become public derived-class members and
+   - protected base-class members become protected derived-class members.

A base class’s private members are never accessible directly in the derived class but can be accessed by calling inherited public and protected base-class member functions designed to access those private members.

When deriving a class with protected inheritance, public and protected base-class members become protected derived-class members. With private inheritance, public and protected base-class members become private derived-class members.

Classes created with private and protected inheritance do not have is-a relationships with their base classes because the base class’s public members are not accessible to the derived class’s client code.

# Default Inheritance in Classes vs. structs

Both class and struct (defined in Section 9.21) can define new types. However, two key differences exist between a class and a struct. The first is that, by default, class members are private, and struct members are public. The other difference is in the default inheritance type. A class definition like

```
```cpp
class Derived : Base {
  // ...
};
```
```