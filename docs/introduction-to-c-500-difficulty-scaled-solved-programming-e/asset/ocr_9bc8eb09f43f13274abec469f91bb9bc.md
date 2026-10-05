# Introduction to C++

Let ask you this. Does the Product class contain a constructor that accepts a Book object as a parameter? No. Then, why the declaration of p is allowed? Because, as we said in Chapter 19, the follow-ing copy constructor is automatically called:

```
Product(const Product&);
```

And as we learned, because the parameter is a reference to the base class it is allowed to refer to a derived class object, and the members of p are initialized with the values of the Product sub-object contained in the b object, which has values AB25 and 8.5, respectively. The derived part of b (e.g., title) is often called class slicing. Similarly, we can assign a derived class to a base class and only the base members are copied. For example:

```
Book b("AB25", 8.5, "Nice", "Many");
Product p;
p = b;
```

The assignment is translated to p.operator=(b), which invokes the Product& operator=(const Product&) function to copy the values of the Product sub-object contained in b into the members of p. As we see in the next section, the reverse b = p; is not automatically allowed, since a Product object is not a Book object.

Finally, we can pass a derived class in a function that accepts a parameter as base class object. For example:

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

When f calls the copy constructor of Product undertakes to copy the Product part of b into p. Therefore, f(b) displays C:AB25 and P:8.5. Like before, the reverse is not allowed, that is, it is not allowed to pass a base class to a function that expects a derived class object.

> When we assign or initialize a base class with a derived class only the members of its sub-object are copied. The rest of the derived object is ignored.

# Conversion from Base to Derived Class

The reverse base-to-derived is not automatically allowed, that is, a reference or pointer to a derived class is not allowed to point to a base class object without type cast. And this is logical, because a base class object does not contain a sub-object of the derived class so that it can be referred or pointed by a pointer to a derived class. Only the reverse is true, as we see in the previous section. For example:

```
Product prod("AB25", 8.5);
Book *p = &prod; // Wrong, it is not allowed to convert a pointer to a base class (e.g., &prod) to the pointer to a derived class (e.g., p). A Product object is not a Book object. */
Book r = prod; // Wrong.
```