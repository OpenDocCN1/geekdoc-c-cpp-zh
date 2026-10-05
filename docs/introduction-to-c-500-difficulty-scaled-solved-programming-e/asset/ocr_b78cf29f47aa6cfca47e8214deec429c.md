20 • Inheritance 651

But, if we use type cast the (Book*) is compiled:

```
Book *p = static_cast<Book*>(&prod);
Book &r = static_cast<Book&>(prod);
```

However, this operation is not safe, because a Product object does not contain a Book sub-object. If we try to access members of the derived class, problems in the execution of the program may occur. For example, if we accidentally write:

```
p->display(); problems may occur since display() is not a member of the Product class.
```

We saw in the previous section that we can assign a derived class object to a base class object. The reverse is not ideal. For example:

```
Book b("AB25", 8.5, "Nice", "Many");
b = p;
```

The assignment is translated to b.operator(p), which invokes the Book& operator=(const Book&) function. Because a reference to a derived class cannot automatically refer to a base class object, this code won't compile. One way to make it work is to overload the assignment operator, that is, our copy function in the Book class to match the argument type. For example:

```
Book& operator=(const Product&) {...}
```

Alternatively, we could define a conversion constructor. For example:

```
Book(const Product&) {...}
```

# DERIVED CLASSES AND COPY OPERATIONS

As we've seen, when a derived object is constructed, the contained base class sub-object is first constructed and then its construction is completed. In the same sense, the copy constructor of a derived class must copy the members of the base sub-object as well as the members of the derived class. The same applies for the copy assignment function of the derived class. The following sections describe these operations in more detail.

# Define a Copy Constructor in a Derived Class

Let's look at a simple inheritance example with default copy constructors:

```
class A
public:
    int r;
    int v;
};
```