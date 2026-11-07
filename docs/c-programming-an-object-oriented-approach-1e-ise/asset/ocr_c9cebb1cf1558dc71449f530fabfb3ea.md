# ### Declaring Static Data Members

Data members belong to the class, and their declarations must be included in the class definition; *static* members must be qualified with the keyword *static*. The following shows how we declare a *static* data member named *count* inside the class definition.

```
~~~cpp
class Rectangle
{
  private:
    ...
    static int count;          // Static data member
  public:
    ...
}
~~~
```

# ### Initializing Static Data Members

We know that an instance data member is normally initialized in a constructor, but a *static* data member belongs to no instance, which means it cannot be initialized in a constructor. A *static* data member must be initialized after the class definition. This means it must be initialized in a global area of the program. We code it after the class definition. We must show that it belongs to the class by adding the class name and the class scope operator (::) to the definition, but the *static* qualifier should not be added. It is already qualified as a *static* data member in the definition section of the class. The following shows how we initialize the *static* member *count*, which is already declared inside the class.

```
~~~cpp
int Rectangle::count = 0;          // initialization of static data member
~~~
```

# ## 7.5.2 Static Member Functions

After declaring and initializing a *static* data member, we must find a way to access it (for example, to print its value). Since a *static* data member is normally *private*, we need a *public* member function to do so. Although this can be done by an instance member function, normally we use a *static* member function for this purpose. A *static* member function can access the *static* data member through an object and also through the name of the class when no object exists. In other words, the use of a *static* member function enables us to access the corresponding *static* data member when an instance wants to access it or when the application needs to access it. Note that a *static* member function has no host object because it is not associated with any instance.

> > **A static member function has no host object.**

# ### Declaring Static Member Functions

A *static* member function, like a *static* data member, belongs to the class. It should be declared inside the class but must be qualified with the keyword *static*. The following shows how we can add a *static* member function *getCount* to retrieve the value of the *static* data member *count* in our *Rectangle* class.