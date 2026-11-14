# ## 2.2.2 Accessibility

Each member of a class has a specified Accessibility. C++ provides three of them:

+   * public: accessible from everywhere;
+   * private: accessible only within the class; and
+   * protected: accessible in the class itself and its derived classes.

This gives the class designer good control of how the class users can work with each member. Defining more public members gives more freedom in usage but less control. On the other hand, more private members establish a more restrictive user interface.

The accessibility of class members is controlled by Access Modifiers. Say we want to implement a class rational with public methods and private data:

```
```cpp
class rational
{
    public:
    ...
    rational operator+(...) {...}
    rational operator-(...) {...}
    private:
    int p;
    int q;
};
```
```

An access modifier applies to all following members until another modifier appears. We can put as many modifiers as we want. Please note our linguistic distinction between a specifier that declares a property of a single item and a modifier that characterizes multiple items: all methods and data members preceding the next modifier. It is better to have many access modifiers than a confusing order of class members. Class members before the first modifier are all private.

# ## 2.2.2.1 Hiding Details

Purists of object-oriented programming declare all data members private. Then it is possible to guarantee properties for all objects, for instance, when we want to establish in the before-mentioned class rational the invariant that the denominator is always positive. Then we declare our numerator and denominator private (as we did) and implement all methods such that they keep this invariant. If the data members were public, we could not guarantee this invariant because users can violate it in their modifications.

private members also increase our freedom regarding code modifications. When we change the interface of private methods or the type of a private variable, all applications of this class will continue working after recompilation. Modifying the interfaces of public methods can (and usually will) break user code. Differently phrased: the public variables and the interfaces of public methods build the interface of a class. As long as we do not change this interface, we can modify a class and all applications will still compile (and work when we did not introduce bugs). And when the public methods keep their behavior, all applications will. How we design our private members is completely up to us (as long as we do not waste