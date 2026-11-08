# Static Member Variables

Static member variables of a class are used to provide class-wide storage of data that is independent of any particular object of the class type but is accessible by any of them. They record properties of the class as a whole, rather than of individual objects. When you declare a member variable of a class as static, the static member variable is defined only once and will exist even if no class objects have been created. Each static member variable is accessible in any object of the class and is shared among however many objects there are. An object gets its own independent copies of the ordinary member variables, but only one instance of each static member variable exists, regardless of how many class objects have been defined.

You can use static member variables to store constants that are specific to a class (see later), or you could store information about the objects of a class in general, such as how many there are in existence. One such use for a static member variable is to count how many objects of a class exist. You could add a static member variable to the Box class by adding the following statement to your class definition (for static member variables we sometimes use a s_ prefix instead of m_):

```
~~~cpp
static inline size_t s_object_count {};  // Count of objects in existence
~~~
```

Figure 12-6 shows how this member exists outside of any objects but is available to all of them.

```
~~~cpp
class Box
{
    ...
private:
    static inline size_t s_object_count {};
    double m_length;
    double m_width;
    double m_height;
}
~~~
```

![](bbox=[0.235, 0.546, 0.802, 0.675])

Figure 12-6. Static class members are shared between objects.

The static `s_object_count` member is private, so you can't access `s_object_count` from outside the *Box* class. Naturally, static members can be either public or protected as well.