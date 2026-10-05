
# ARRAY OF OBJECTS

An array of objects is an array whose elements are objects. For example, in the program C.17.1 the statement:

Student s[10]; declares s as an array of ten elements, where each element is a Student object. The default constructor is called for each object created, that is, called ten times. In general, we can use the same or different constructors to initialize an array. For example:

```cpp
#include <iostream> // Example 17.13
```

```cpp
class Test {
public:
    int a, b;
    Test() {a=b=1};
    Test(int i, int j) {a=i; b=j};
};
```

```cpp
int main() {
    int i;
    Test t[10] = {Test(1, 2), Test(), Test(5, 6)};

    for(i = 0; i < 10; i++)
        std::cout << t[i].a << ' ' << t[i].b << '\n';

    return 0;
}
```

The second constructor is called for t[0] and t[2], while the default constructor is called for t[1]. Because the initialization list is shorter than the number of elements, the default constructor is called for the remaining seven objects. If it was missing, the compiler would display an error message. The program displays the values of the members of each object.

And if we write: Test *p = new Test[3]; which constructor will be called? The default. How many times? Three, for each object. How about if the default constructor was missing? In that case, we should use the constructor. Here is an initialization example:

```cpp
Test *p = new Test[3]{{1, 2}, {3, 4}, {5, 6}}; /* The a and b of the first object become 1 and 2, respectively. Similarly, for the other two objects. */
```

When we write delete[p]; which function will be called? The default destructor, again three times. In which order? As we've said, the destructor is called in reverse order from the construction order, that is, p[2] will be destroyed first and p[0] last.

Alternatively, as we know, we can use a vector object with elements of type Test. For example:

```cpp
int main() {
    int i;
    std::vector<Test> v;
    Test t1(2
for(i = 0; i < v.size(); i++)
    std::cout << v[i].a << ' ' << v[i].b << '\n';
return 0;
}
```

# CLASS CONSTANTS

When declaring a class we may want to use some constants. We could use global variables, but since they will be used only inside the class it fits to the encapsulation philosophy to define them inside the class. For example, suppose we want to use a constant to specify the size of an array. Because this constant is the same for all objects, it would be created once and shared by all the objects. For example, we'd write something like:

```cpp
class T
private:
    const int SIZE = 10;
    int arr[SIZE]; // Wrong.
...;
```

in the SIZE variable to be created and shared by all T objects. However, this is not allowed, because the declaration of a class does not create object to reserve memory for SIZE and its value, it describes the structure of the class. What can we do? One way to define a constant within a class is to declare an enumeration. For example:

```cpp
class T
private:
    enum {SIZE = 10};
    int arr[SIZE];
...;
```

The enumeration does not create member of the class. The enumeration is not contained in every object of class T. Simply put, SIZE is a symbolic name and each time the compiler encounters it within the scope of the class, it replaces it with 10.
Another way is to use a static constant. In fact, static members are typically used to define constants. This makes sense, since there is no need to create a copy of the same constant variable each time an object is created. By defining it as static, only one instance of this constant will be created and shared among the objects. As I've mentioned, I prefer to write the constants in capital letters so that they stand out in the program.

```cpp
#include <iostream> // Example 17.14
class T
public:
    static int SIZE = 10; // Wrong, it is not const.
    static const int SIZE = 10; // OK. We can also use constexpr instead of const.*
    int arr[SIZE];
    void f();
;
```

```cpp
void T::f()
{
    for(int i = 0; i < SIZE; i++)
        arr[i] = i+SIZE;
    std::cout << arr[SIZE-1] << '\n';
}
```

```cpp
int main()
{
    T t;
    t.f();
    std::cout << SIZE << '\n'; // Wrong, out of scope.
    return 0;
}
```

Now, only one constant named SIZE is created, which is shared by all T objects. As we see in the next section, SIZE is not stored in each object but in the same memory area where SIZE is visible within the scope of the class and to f() outputs 19. The comment says, if you try to use it outside of class, the compiler will display an error message. If you use the scope operator or T::SIZE there will be no problem.

Regarding the initialization there are some restrictions. For example, the type of the static constant must be an integer or enumeration or a constexpr expression and the initial value must be constant.

```cpp
class T
{
    static const int PI = 3; // OK.
    static const float PI = 3.14; // Wrong.
    static constexpr float PI = 3.14; // OK.
}
```

The initialization rules are simplified with C++17 and the introduction of the inline variables. It allows us to initialize the variable irrespective of its type. For example, we can write:

```cpp
class T
{
    static inline const float PI = 3.14; // OK, since C++17.
}
```

The order of the static, inline, and const keywords does not matter.

# STATIC MEMBER VARIABLES

When we want to declare a variable in a class that is shared by all the objects of the class we declare it as static. A static member is created once and shared by all the objects. It belongs to the class as a whole, not to a particular object. To show you an example, let's declare the test.h:

```cpp
#ifndef TEST_H
#define TEST_H

class T
{
private:
    int v;
    double d;
public:
    static int num; // Declare the static variable.
    void set() {v = num};
}

#endif
```

```cpp
#include <iostream> // Example 17.15
#include "test.h"

int T::num = 5; // Define the static variable.
```

```cpp
int main() {
    T t[10];

    t[2].num = 20; // Alternately, T::num = 20;
    std::cout << t[5].num << '\n';
    return 0;
}
```

The memory for such static variables is reserved when the program begins, as global variables. Thus, num will be defined, that memory is reserved for it, even if no object is created. If you do not assign an initial value to it, int T::num becomes 0. Class members (e.g., set()) can access static variables directly, without using the :: operator.

We also see that the static variable is not a discrete member of the object, we can use an object, such as t[2] (or pointer or object reference), to access it. In order to make clear that the variable is static, I prefer to use the syntax with the class and the :: operator (e.g., T::num).

As we said, a static constant can be initialized within the class. This is not allowed for a non-constant static variable, though it must be defined outside the class. C++17 relaxes this requirement and simplifies the definition with the introduction of the inline variables. In particular,
