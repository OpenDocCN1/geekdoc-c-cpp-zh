```
...    // other special member functions due to the problem of slicing
};
```

In this base class, move semantics is disabled, which means that if we move a geometric object the members declared here in the base class have no automatic support for move semantics. This also applies if we have a protected copy constructor and a deleted assignment operator, which you should usually have in a polymorphic base class to avoid the problem of slicing.

As long as the base class does not introduce members, not supporting move semantics has no effect. However, if we have an expensive member in this base class, you have disabled move support for it. For example:

```
class GeoObj {
protected:
    std::string name;                // name of the geometric object
public:
    ...
    virtual void draw() const = 0;   // pure virtual function (introducing the API)
    ...
    virtual ~GeoObj() = default;     // disables move semantics for name
    ...    // other special member functions due to the problem of slicing
};
```

To enable move semantics again, you can explicitly declare the move operations as defaulted. However, as we have just learned, this disables the copying special member functions. Therefore, if you want to have these functions, you have to provide them explicitly.

# Dealing with Slicing

However, there is the problem of slicing. Consider the following code using a reference of the base class GeoObj for objects of the derived class Circle:

```
Circle c1{...}, c2{...};

GeoObj& geoRef{c1};
geoRef = c2;    // OOPS: uses GeoObj::operator=() and assigns no Circle members
```

Because we call the assignment operator for a GeoObj and the operator is not virtual, the compiler calls GeoObj::operator=(), which does not deal with any member of any derived class. Even declaring the assignment operator with virtual would not help, because an operator of the derived class does not override the assignment operator of the base class (the parameter types for the second operand differ).

To avoid this problem, you should disable the use of the assignment operator in polymorphic class hierarchies. Furthermore, if the class is not abstract, you should also avoid having public copy constructors to disable implicit type conversions to the base class. Therefore, a polymorphic base class with move semantics (and members) should be declared as follows:

```
class GeoObj {
protected:
    std::string name;                // name of the geometric object
```