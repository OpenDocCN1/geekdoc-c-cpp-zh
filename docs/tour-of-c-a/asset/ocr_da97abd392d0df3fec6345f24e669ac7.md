This Container can be used like:

Click here to view code image

```
void use(Container& c)
{
    const int sz = c.size();
    for (int i=0; i<sz; ++i)
        cout << c[i] << "\n"
}
```

Note use() the Container interface in complete ignorance of implementation details. It uses size() and [] to be away of exactly which type provides their implementation. A class that provides the interface to a variety of other classes is often a polymorphic type.

As is common for abstract classes, Container does not have a constructor. After all, it does not have any data to initialize. On the other hand, Container has a destructor and destructor is virtual, so that classes derived from Container can provide implementations. Again, that is for abstract classes because they tend to be manipulated by references or pointers, and destroying some Container through a pointer has no what resources are owned by its implementation; see also $5.5.

The abstract class Container defines only an interface and no implementation. For Container to be useful, we have to implement it and the functions required by its interface. For that, we use the concrete class Vector.

Click here to view code image

```
class Vector_container : public Container {\ II Vector_container implements Container
public:
    Vector_container(int s) : v(s) {} II Vector of elements
    Vector_container() {}
private:
    double& operator[](int i) i override { return v[i]; }
    int size() const override { return v.size(); }
    Vector v;
};
```

The public can be read as "derived" or "is a subtype of" Class Vector_container is said to be derived from class Container and class Container is said to be a base of class Vector_container. An alternative terminology calls Vector_container and Container subclass and superclass, respectively. The class is said to inherit members from its base class, so the use of derived classes is commonly referred to as inheritance.

The members operator[] and size() are said to override the corresponding members in the base class Container. I use explicit override to make clear what is intended. The use of override is optional, but being explicit allows the compiler to catch mistakes, such as misspellings of function names or slight differences between the type of a virtual function and its intended override. The explicit override is particularly useful in larger class hierarchies where it can otherwise be hard to know what is supposed to override what.

The destructor (~Vector_container()) overrides the base class destructor (~Container()). Note that the member destructor (~Vector()) is implicitly invoked by its class's destructor (~Vector_container()).