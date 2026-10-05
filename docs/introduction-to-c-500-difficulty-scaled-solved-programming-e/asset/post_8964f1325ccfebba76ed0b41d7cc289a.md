
18 • Operator Overloading 567

Now, we can write in main():

```
int main()
{
    Rect r(10, 20);

    (-r).show(); /* Since the function returns a reference to Rect object,
    we can call show(). */
    return 0;
}
```

As I said, when you overload an operator, it is very important to make the code easier to read and understand. In this example, someone who reads the code cannot figure out that the -r expression swaps the dimensions. It'd be better to define a function with a relevant name (e.g., swap) and call that function instead. Here, it is just an example of how to overload a unary operator.

## Overloading the ++ and -- Operators

Let's overload the ++ operator, is overloaded in a similar way, to increase the dimensions of the invoking object. As we know, the ++ operator can be applied in two ways. Therefore, we'll implement two versions of the function, one for the postfix and one for the prefix increment. For example, with the statement ++r; the function should return the object after increasing its dimensions, while with r++; return r before increasing its dimensions. Fine, but there is a problem. Since both functions have the same name operator and do not accept parameters, that is, they have the same signature, how will the compiler figure out which one to call? To solve this, an integer is added in the postfix version. For example:

```
Rect::operator++() /* Prefix version (e.g., ++r). The declaration is added in the class. */
{
    length++;
    height++;
    return *this;
}
```

```
Rect::operator++(int) /* Postfix version (e.g., r++). The declaration is added in the class. */
{
    Rect tmp;
    tmp = *this;
    length++;
    height++;
    return tmp;
}
```

In the postfix version the argument is not used, and therefore its name is not needed. It is just a dummy argument that the compiler uses to distinguish which version to call. Also, the prefix version normally returns a reference to the current object, while the postfix returns a copy of the original object, not a reference. See main():

```
int main()
{
    Rect r1(10, 20), r2, r3;

    r2 = ++r1; // Equivalent to r2 = r1.operator++();
    r1.show(); // The Program outputs 11 21
    r2.show(); // The Program outputs 11 21

    r3 = r1++; // Equivalent to r3 = r1.operator++();
    r1.show(); // The Program outputs 12 22
    r3.show(); // The Program outputs 11 21

    return 0;
}
```

In the postfix version the compiler passes a dummy argument (e.g., the value). To ask you, let's say that we just want to increase the dimensions of r1. Which of the two is more efficient? To answer, the prefix version is more efficient because the object pointed to by this is not copied. In the general, said, the -- operator is not overloaded in the same way, we replace increments with decrements in both postfix and prefix versions. A typical use of ++ and -- overloading is in standard library classes to iterators. We've seen such an example in Chapter 7.

## Overloading the -> and * Operators

Let's see an example of the -> operator, which can be defined as a unary operator. As in the overloading restrictions, the overloaded function of -> must be a class member:

```
#include <iostream> // Example 18.3
class A
{
public:
    void f() const { std::cout << "One\n"; }
};

class T
{
private:
    A a;
public:
    A* operator->();
};

A* T::operator->()
{
    return &a;
}
```

```cpp
int main()
{
    T t;
    t->f(); // Equivalent to (t.operator())->f();
    return 0;
}
```

Let's see how the program works. To clarify, the program has no practical value; it is just an example of -> overloading. The expression t->f() triggers the call of t.operator->(), which returns a pointer to the object. Then, f() is called, which displays One. So, this shows that a T object can access members of the class in a similar way to a pointer. Note that although it can be overloaded, its purpose cannot change. That is, a class member must be specified of the right of and is used to access it. Now that we have learned that the operator -> can be overloaded, the expression t->field in the general case, is equivalent to:

- a) (*ptr->field) If ptr is a pointer to object
- b) (ptr.operator()->field) If ptr is an object of a class

If the function returns a pointer the field is accessed again, recursively, until a pointer is returned to the indicated member or some other value, in which case a compilation error will occur. Because the syntax of -> does not change, a member name is renamed after it. For example:

```
A* p = t--; // Wrong.
A* p = t.operator->(); // OK.
```

Although it may seem that the overloading of -> is just a special case rarely needed, it may be useful in certain applications, such as the implementation of "smart" pointers as we'll see in Chapter 25, objects that behave like pointers. To overload the dereference operator we should define the operator* function. Don't forget that it is useful for the better comprehension and maintenance of the program when an operator is overloaded to perform a similar function to its original purpose. Consider the following program:

```
#include <iostream> // Example 18.4
class T {
private:
    int arr[10];
public:
    int& operator*() const {return arr[0];};
};

int main()
{
    T t;
    *t = 20; // Equivalent to t.operator*() = 20;
    return 0;
}
```

The expression *t = 20; triggers the call of t.operator*(), which returns a reference to arr[0]. Then, its value becomes 20.

## Overloading the [] Operator

Although the [] operator is not a conventional unary operator such as ++ I'd like to add an example of its use because it is a particularly useful operator that is often overloaded. As we saw in the overloading restrictions, the overloaded function of [] must be a class member. Let's look at a simple example of a class that returns an array:

```cpp
class Array // Example 18.5
private:
    int arr[10];
public:
    int& operator[](int i);
};
int& Array::operator[](int i)
{
    return arr[i]; /* For simplicity, it is not checked if the value of i is within valid range. In exercise U.18.2 you'll be asked to do it. */
}
```

```cpp
int main()
{
    Array a;
    a[0] = 5; /* Equivalent to a.operator[](0) = 5. The a.arr[0] becomes 5.
    return 0;
}
```

Usually, the operator[] function is defined to return a reference to the element and not its value, in order work like l[i]. For example, if we have an array, we can write b[3] = i; and i = b[3]. Usually, we want the operator[] to support this. To achieve this, we declare the function to return a reference so that when the operator [] is used at the left we can assign a value to a particular element. When the function is called, the value inside the brackets becomes its assignment. For example, the statement a[0] = 5 invokes the a.operator[](0), which returns a reference to arr[0]. Thus, the value of arr[0] becomes 5.

Note that if the type was just int the compiler would display an error message that the assignment of operand is not allowed. That is, we could only read the value of the element (e.g., int c = a[0]); and not write to it.
