
In this example, the addition operator (`+`) has a lower precedence than the multiplication operator (`*`), so the expressions within the parentheses are evaluated first. The addition operator (`+`) is left-associative, so `x` and `y` are added first, then `z` and `1` are added. The result of these additions is then multiplied to produce the final result.

### what is Casting

In C++, casting is the process of converting a value of one type to a value of another type. There are several ways to perform casting in C++:

- 1. Static cast: The `static_cast` operator is used to perform a safe, explicit type conversion. It can be used to convert a value from one type to another, as long as the target type is explicitly specified. For example:

```
double x = 3.14;

int y = static_cast<int>(x); // y is 3
```

- 2. Dynamic cast: The `dynamic_cast` operator is used to perform a type conversion at runtime. It is used to convert a pointer or reference from a base class type to a derived class type. For example:

```
class Base { };

class Derived : public Base { };
```

```
Base *b = new Base();

Derived *d = dynamic_cast<Derived*>(b); // d is nullptr
```

- 3. Reinterpret cast: The `reinterpret_cast` operator is used to interpret the bits
of a value as a value of a different type. It is used to convert a pointer to an integer type, or vice versa. For example:

```
int x = 42;

char *ptr = reinterpret_cast<char*>(&x); // ptr points to the first byte of x
```

- 4. Const cast: The `const_cast` operator is used to remove the `const` qualifier from a value. It is used to modify a `const` value, or to pass a `const` value to a function that expects a non-`const` parameter. For example:

```
const int x = 42;

int *ptr = const_cast<int*>(&x); // ptr points to x, but x can be modified through ptr
```

It is important to note that casting can sometimes result in loss of information or undefined behavior if the target type is not capable of representing the value being converted. Therefore, it is important to use casting cautiously and only when necessary.

## seventh chapter

### Casting operators

In C++, casting refers to the process of converting a value of one data type to another data type. This can be done using a variety of casting operators, including:

- 1. `static_cast` : This operator is used to perform a safe, explicit type conversion. It can be used to convert values between compatible types, such as converting an `int` to a `float` .
- 2. `dynamic_cast` : This operator is used to perform a safe, downcast conversion from a base class to a derived class. It is used when the type of the object being converted is not known at compile-time, and is typically used in conjunction with polymorphism.
- 3. `const_cast` : This operator is used to remove the `const` or `volatile` attribute from a variable. It can be used to cast away the `const` or `volatile` qualifier from a pointer or reference, allowing the value to be modified.
- 4. `reinterpret_cast` : This operator is used to perform a low-level, implementation-defined type conversion. It can be used to convert a value of one type to a value of a different type, regardless of whether the two types are related. This operator is generally used to cast pointers to and from integer types, or to cast one pointer type to another.

It's important to note that these casting operators can often result in undefined behavior if used improperly, so they should be used with caution.

### dynamic_cast operator

The `dynamic_cast` operator in C++ is used to perform a safe, downcast conversion from a base class to a derived class. It is typically used in conjunction with polymorphism, where a pointer or reference to a base class is used to refer to objects of derived classes.

The syntax for using `dynamic_cast` is as follows:

```
derived_type *ptr = dynamic_cast<derived_type*>(base_ptr);
```

Where `derived_type` is the type of the derived class and `base_ptr` is a pointer to the base class. If the conversion is successful, `dynamic_cast` will return a pointer to the derived class. If the conversion is not possible (for example, if `base_ptr` does not actually point to an object of the derived class), `dynamic_cast` will return a null pointer.

Here is an example of using `dynamic_cast` to downcast a pointer to a base class:

```
#include <iostream>

class Shape {

public:

    virtual ~Shape() {}

};

class Circle : public Shape {

public:

    void Draw() { std::cout << "Drawing a circle" << std::endl; }

};

int main() {

    Shape *shape = new Circle;

    Circle *circle = dynamic_cast<Circle*>(shape);

    if (circle != nullptr) {

        circle->Draw();

    } else {

        std::cout << "Error: shape is not a circle" << std::endl;

    }

    return 0;

}
```

In this example, the `dynamic_cast` operator is used to downcast a pointer to a Shape object to a pointer to a Circle object. If the Shape object is actually a Circle, the conversion will succeed and the Draw method will be called on the Circle object. If the Shape object is not a Circle, the `dynamic_cast` operator will return a null pointer and the Draw method will not be called.

### bad_cast exception

The `bad_cast` exception is a type of exception that is thrown by the `dynamic_cast` operator in C++ when it fails to perform a downcast conversion from a base class to a derived class.

The `bad_cast` exception is defined in the `stdexcept` header and is derived from the `exception` class. It can be caught using a try - catch block, like any other exception:

```
#include <iostream>

#include <stdexcept>

int main() {

    try {

        Shape *shape = new Shape;

        Circle *circle = dynamic_cast<Circle*>(shape);

    } catch (std::bad_cast& e) {

        std::cout << "Error: " << e.what() << std::endl;

    }

    return 0;

}
```

In this example, the `dynamic_cast` operator will fail to convert the Shape object to a Circle object, and will throw a `bad_cast` exception. The exception will be caught in the catch block, and the error message will be printed to the console.

It's important to note that the `bad_cast` exception will only be thrown if the `dynamic_cast` operator fails to perform the conversion. If the conversion is successful, the `bad_cast` exception will not be thrown.

### static_cast operator

The `static_cast` operator in C++ is used to perform a safe, explicit type conversion. It can be used to convert values between compatible types, such as converting an `int` to a `float`, or to convert a pointer to a base class to a pointer to a derived class.

The syntax for using `static_cast` is as follows:

```
destination_type value = static_cast<destination_type>(expression);
```

Where `destination_type` is the type to which the value of `expression` will be converted, and `expression` is the value to be converted.

Here is an example of using `static_cast` to convert an `int` to a `float` :

```
#include <iostream>

int main() {

    int x = 5;

    float y = static_cast<float>(x);

    std::cout << "y = " << y << std::endl;

    return 0;

}
```

In this example, the value of `x` is converted from an `int` to a `float` using the `static_cast` operator, and the result is stored in the `float` variable `y`. The output of this program will be "y = 5.0".

It's important to note that `static_cast` does not perform any runtime checks to ensure that the conversion is valid. It is the responsibility of the programmer to ensure that the conversion is safe and will not result in undefined behavior.

### const_cast operator

The `const_cast` operator in C++ is used to remove the `const` or `volatile` attribute from a variable. It can be used to cast away the `const` or `volatile` qualifier from a pointer or reference, allowing the value to be modified.

The syntax for using `const_cast` is as follows:

```
destination_type value = const_cast<destination_type>(expression);
```
