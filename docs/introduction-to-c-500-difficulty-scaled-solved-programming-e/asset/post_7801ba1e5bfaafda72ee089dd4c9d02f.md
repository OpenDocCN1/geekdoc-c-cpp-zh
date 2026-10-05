
# Introduction to C++

Let me ask you this: does the Product class contain a constructor that accepts a Book object as a parameter? No. Then, why is the declaration of p allowed? Because, as we said in Chapter 19, the following copy constructor is automatically called:

```
Product(const Product&);
```

And as we learned, because the parameter is a reference to the base class, it is allowed to refer to a derived class object, and the members of p are initialized with the values of the Product sub-object contained in the b object, which has values AB25 and 8.5, respectively. The derived part of b (e.g., title) is often called class slicing. Similarly, we can assign a derived class to a base class and only the base members are copied. For example:

```
Book b("AB25", 8.5, "Nice", "Many");
Product p;
p = b;
```

The assignment is translated to p.operator=(b), which invokes the Product& operator=(const Product&) function to copy the values of the Product sub-object contained in b into the members of p. As we see in the next section, the reverse b = p; is not automatically allowed, since a Product object is not a Book object.

Finally, we can pass a derived class in a function that accepts a parameter as a base class object. For example:

```
void f(Product p)
{
    p.show();
}
```

```
Book b("AB25", 8.5, "Nice", "Many");
f(b); // The Book object is also a Product object.
```

When f calls the copy constructor of Product, it undertakes to copy the Product part of b into p. Therefore, f(b) displays C:AB25 and P:8.5. Like before, the reverse is not allowed; that is, it is not allowed to pass a base class to a function that expects a derived class object.

> When we assign or initialize a base class with a derived class, only the members of its sub-object are copied. The rest of the derived object is ignored.

# Conversion from Base to Derived Class

The reverse base-to-derived is not automatically allowed; that is, a reference or pointer to a derived class is not allowed to point to a base class object without type cast. And this is logical, because a base class object does not contain a sub-object of the derived class so that it can be referred or pointed to by a pointer to a derived class. Only the reverse is true, as we see in the previous section. For example:

```
Product prod("AB25", 8.5);
Book *p = &prod; // Wrong, it is not allowed to convert a pointer to a base class (e.g., &prod) to the pointer to a derived class (e.g., p). A Product object is not a Book object.
Book r = prod; // Wrong.
```

But, if we use type cast, the (Book*) is compiled:

```
Book *p = static_cast<Book*>(&prod);
Book &r = static_cast<Book&>(prod);
```

However, this operation is not safe, because a Product object does not contain a Book sub-object. If we try to access members of the derived class, problems in the execution of the program may occur. For example, if we accidentally write:

```cpp
p->display(); // problems may occur since display() is not a member of the Product class.
```

We saw in the previous section that we can assign a derived class object to a base class object. The reverse is not ideal. For example:

```
Book b("AB25", 8.5, "Nice", "Many");
b = p;
```

The assignment is translated to b.operator=(p), which invokes the Book& operator=(const Book&) function. Because a reference to a derived class cannot automatically refer to a base class object, this code won't compile. One way to make it work is to overload the assignment operator, that is, our copy function in the Book class to match the argument type. For example:

```cpp
Book& operator=(const Product&) {...}
```

Alternatively, we could define a conversion constructor. For example:

```cpp
Book(const Product&) {...}
```

# DERIVED CLASSES AND COPY OPERATIONS

As we've seen, when a derived object is constructed, the contained base class sub-object is first constructed and then its construction is completed. In the same sense, the copy constructor of a derived class must copy the members of the base sub-object as well as the members of the derived class. The same applies for the copy assignment function of the derived class. The following sections describe these operations in more detail.

# Define a Copy Constructor in a Derived Class

Let's look at a simple inheritance example with default copy constructors:

```cpp
class A
public:
    int r;
    int v;
};
```

```cpp
class B : public A
{
    ...
};

int main()
{
    B b;
    b.r = 10;
    A a = b;
}
```

Let's see a more complex example. The following program is an example of how to define your own copy constructors in a derived class and its base class:

```cpp
#include <iostream> // Example 20.6

class A
public:
    int a;
    A(int i) : a(i) {}
    A(const A& r) : a(r.a + 1) {}

class B : public A
private:
    int t;
public:
    B(int i) : A(i), t(i+20) {}
    B(const B& b) : A(b), t(b.t + 1) {}
    void show() const { std::cout << a << '\n'; }

int main()
{
    B b1(10);
    B b2 = b1;
    b2.show();
    return 0;
}
```

The constructor of the derived class B calls the constructor of the base class. When the b1 object is created, the value of the member of the A sub-object contained in b1 becomes 10 and the value of b.t becomes 30.

Let's now look at the calls of the copy constructors to b2. In general, when we define a copy constructor in a derived class and want to use the default copy constructor in the base class, we must call it in the initialization list. Thus, when b2 is created, the constructor of B is called, which in turn calls the copy constructor of A.

> When we assign or initialize a base class with a derived class only the members of its sub-object are copied. The rest of the derived object is ignored.

# FUNCTION REDFINITION

As we already know, an object of a derived class can use functions of the base class to behave differently in the derived class, which means to have multiple forms of the same function (polymorphism). Thus, the way a particular function behaves depends on the object it calls. To achieve polymorphism we must redefine the function in the derived class. There are two situations to explore. The first one is when the functions have the same signature and the second one with different signatures.

# Function Redefinition with Same Signature

As an example, the C.20.1 program with the Product and Book classes. Let's change the name of the (display) function in the Book class to show() and write the following code:

```cpp
void Book::show() const
{
    cout << "T:" << title << "A:" << auth << '\n';
}
```

We have two versions of show(), one in the base class and one in the derived.

```cpp
Product p("A", 1);
Book b("B", 2, "Nice", "Many");
p.show(); // The Product::show() is called.
b.show(); // The Book::show() is called.
```

the compiler checks the type of the object to decide which of the two versions to call. Essentially, when a base class function is redefined in a derived class, the derived class function hides the base class function.
