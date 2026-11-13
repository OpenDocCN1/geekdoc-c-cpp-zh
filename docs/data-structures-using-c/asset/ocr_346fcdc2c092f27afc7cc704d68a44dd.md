We can define a general class that has common features related to a set of items. This class is called superclass or base class. A derived class inherits some or all the features of the base class. The superclass can be inherited by other classes, which can add their own unique features to it. These classes are called subclass or derived class. The syntax for a derived class is given as follows:

```
class derived class name: access right Base class name
{
    ...
}
```

The phrase ‘inherits from’ is replaced by a colon in class definition. As an example, let us design a class for 3D points using the already existing class Point. Access right is also referred as visibility mode. The visibility mode is optional and if present may be either public or private. Visibility mode specifies whether the characteristics of the base class are privately or publicly derived.

```
class Point3D:public Point
{
    int _z;
    public:
    Point3D()
    {
        setX(0);
        setY(0);
        _z = 0;
    }
    Point3D(const int x, const int y, const int z)
    {
        setX(x);
        setY(y);
        _z = z;
    }
    ~Point3D()({ /* Nothing to do *\/
    int getZ(){return _z;}
    void setZ(const int val){_z = val;}
};
```

# A.10.1 Types of Inheritance

In the definition, the keyword public is used in the first line of the class definition as its signature. This is necessary because C++ distinguishes two types of inheritance, public and private. By default, classes are privately derived from each other. We need to explicitly instruct the compiler to use public inheritance.

The type of inheritance influences the access rights to the elements of the base class. Using public inheritance, everything that is declared private in a base class remains private in the subclass. Similarly, everything that is public remains public. When using private inheritance, the features are quite different as shown in Table A.1.