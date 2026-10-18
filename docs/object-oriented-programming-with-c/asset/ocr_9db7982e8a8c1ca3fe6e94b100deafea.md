```
```cpp
~A()
{
    //Base class destructor
};

class B : public A
{
public:
    ~B()
    {
        //Derived class destructor
    }
};

main()
{
    A *ptr = new B();
    delete ptr;
}
```
```

In the above class declarations, both base class A and the derived class B have their own destructors. Now, an A class pointer has been allocated a B class object. When this object pointer is deleted using the delete operator, it will trigger the base class destructor and the derived class destructor won’t be called at all. This may lead to a memory leak situation. To make sure that the derived class destructor is mandatorily called, we must declare the base class destructor as virtual, as shown below.

```
```cpp
class A
{
public:
    virtual ~A()
    {
        //Base class destructor
    }
};
```
```

# Summary