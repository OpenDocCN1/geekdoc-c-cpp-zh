# 17 • Classes and Objects 537

```
for(i = 0; i < v.size(); i++)
std::cout << v[i].a << ' ' << v[i].b << '\\n';
return 0;
}
```

# # CLASS CONSTANTS

When declaring a class we may want to use some constants. We could use global variables, but since they will be used only inside the class fits to the encapsulation philosophy to define them inside the class. For example, suppose we want to use a constant to specify the size of an array. Because this constant is the same for all objects, it would be created once and shared by all the objects. For example, we'd write something like:

```
class T
private:
    const int SIZE = 10;
    int arr[SIZE]; // Wrong.
...;
```

in the SIZE variable to be created and shared by all T objects. However, this is not allowed, because the declaration of a class does not create object to reserve memory for SIZE and its value, it describes the structure of the class. What can we do? One way to define a constant within a class is to declare an enumeration. For example:

```
class T
private:
    enum {SIZE = 10};
    int arr[SIZE];
...;
```

The enumeration does not create member of the class. The enumeration is not contained in every object of class T. Simply put, SIZE is a symbolic name and each time the compiler encounters it within the scope of the class, it replaces it with 10.
Another way is to use a static constant. In fact, static members are typically used to define constants. This makes sense, since there is no need to create a copy of the same constant variable each time an object is created. By defining it as static, only one instance of this constant will be created and shared among the objects. As I've mentioned, I prefer to write the constants in capital letters so that they stand out in the program.

```
#include <iostream> // Example 17.14
class T
public:
    static int SIZE = 10; // Wrong, it is not const.
    static const int SIZE = 10; // OK. We can also use constexpr instead of const.*
    int arr[SIZE];
    void f();
;
```