default values of 1.0. The next statement shows that the accessor functions are inherited too and can be called for a derived class object.

Uncommenting either of the last two statements results in an error message from the compiler. The member variables that are inherited by the Carton class are private in the base class, and they are still private in the derived class, Carton, so they cannot be accessed from outside the class. There’s more, though. Try adding this function to the Carton class as a public member:

```
```cpp
double cartonVolume() const { return m_length * m_width * m_height; }
```
```

This won’t compile. The reason is that although the member variables of Box are inherited, they are inherited as private members of the Box class. The private access specifier determines that these members are totally private to the class. Not only can they not be accessed from outside the Box class, they also cannot be accessed from inside a class that inherits them.

Access to inherited members of a derived class object is not only determined by their access specification in the base class but by both the access specifier in the base class and the access specifier of the base class in the derived class. We’ll go into that a bit more next.

# Protected Members of a Class

The private members of a base class being only accessible to member functions of the base class can be, to say the least, inconvenient. Often you want the members of a base class to be accessible from within the derived class but nonetheless protected from outside. In addition to the public and private access specifiers for class members, you can declare members as protected. Within the class, the protected keyword has the same effect as the private keyword. protected members cannot be accessed from outside the class except from functions that have been specified as friend functions. Things change in a derived class, though. Members of a base class that are declared as protected are freely accessible in member functions of a derived class, whereas the private members of the base class are not.

We can modify the Box class to have protected member variables:

```
```cpp
class Box
{
public:
    // Rest of the class as before...

protected:
    double m_length {1.0};
    double m_width {1.0};
    double m_height {1.0};
};
```
```

The member variables of Box still cannot be accessed by ordinary global functions, but they are now accessible within member functions of a derived class.

> **Tip**  Member variables should normally always be private. The previous example was just to indicate what is possible. In general, protected member variables introduce similar issues as public member variables, only to a lesser extent. We’ll explore this in more detail in the next section.