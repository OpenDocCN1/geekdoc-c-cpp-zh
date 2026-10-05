# 25 • Namespaces, Type Cast Operators, and Smart Pointers 821

Because the cast is not safe, the `bad_cast` exception is thrown, which is captured by the respective catch block.

# The typeid Operator

The `typeid` operator is used to determine the type of an object. It returns a reference to a `type_info` object, as its name suggests, holds information about the type of the passed argument. The `type_info` class is declared in the `typeinfo` file. In its usual use, `typeid` takes as a parameter the name of a class or an expression that is evaluated to an object. If it is a type (e.g. int) the returned value represents the type. If it is an expression identifies a polymorphic class (a class with least one virtual function), the returned value represents the dynamic type of the expression. Otherwise, if the expression identifies a non-polymorphic class, the returned value represents the static type of the expression. The `type_info` class overloads the `==` and `!=` to compare types. For example, let's use the previously defined `A`, `B`, and `C` classes:

```
#include <iostream> // Example 25.5
#include <typeinfo>
int main() {
    B *p = new C;
    C *c;
    A& r = c;

    try {
        if (typeid(C) == typeid(*p)) /* Compare with the type of the object p points to. */ {
            p->show();
            std::cout << typeid(*p).name() << '\n';
        }
        if (typeid(C) == typeid(r)) /* Compare with the type of the object r refers to. */ {
            r.show();
        }
    } catch (std::bad_type&)\ {
        std::cout << "bad_type exception is caught\n";
    }
    delete p;
    return 0;
}
```

Since C is polymorphic, the first `if` condition checks the type of the object that p points to. Since it points to an object of the C class, the condition is true and the program displays C. Because C class is polymorphic the `*p` is evaluated at runtime. If p is a null pointer, `typeid(*p)` throws the `bad_type` exception. This exception is derived from the exception class and is declared in the `typeinfo` file. Also, the `type_info` class contains the `name()` function, which returns a C string that refers to the name of the type and uses the same name as the class. For example, with the compiler I used the program displays `Class C`. Then, because C is polymorphic the second `if` condition is true and because `show()` is virtual the program displays C.