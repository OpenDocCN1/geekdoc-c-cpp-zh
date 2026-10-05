```
;
void main()
{
    B Bi;    //ERROR!
}
```

Next, a class C derives from class B. It overrides and defines the remaining virtual functions of class A. Thus, class C becomes a concrete class. See Listing 6.19.

| Listing 6.19 Defining all the inherited pure virtual functions results in a concrete class |

```
class C : public B
{
public:
    void def()
    {
        //definition of C::def() function
    }
    void ghi()
    {
        //definition of C::ghi() function
    }
};
void main()
{
    C C1; //OK
}
```

We may ask why all virtual functions of class A were not defined in class B itself. The reason is that there is no concrete definition of the remaining functions with respect to class B. It serves as a base class for a number of derived classes. Each of the derived classes have a different definition of the pure virtual functions of class A that are undefined by class B. If class B defines any of these functions, then functions will be called when a pointer of class A points to an object of the derived classes of class B and calls are dispatched to the pure virtual function of class A. This is obviously undesirable. Class B will only define those pure virtual functions of class A that can have a suitable meaning with respect to it. Such definitions will be applicable to all its derived classes.

Although concrete classes must provide an implementation to all the pure virtual functions, the abstract data type may provide one as well. The derived class can invoke it by using the scope resolution operator (Listing 6.20).

| Listing 6.20 Defining a pure virtual function in the abstract base class itself |

```
class A
{\public:
    virtual void abc()=0;//An abstract base class
};
void A::abc() //pure virtual function defined
{
    //definition of A::abc() function
}
```