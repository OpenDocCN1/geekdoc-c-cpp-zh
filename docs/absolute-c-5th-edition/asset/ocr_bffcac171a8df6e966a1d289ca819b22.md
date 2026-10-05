# 15.2 Pointers and Virtual Functions

> Beware lest you lose the substance by grasping the shadow.

AESOP, The Dog and the Shadow

This section explores some of the more subtle points about virtual functions. To understand this material, you need to have covered the material on pointers in Chapter 10.

# Virtual Functions and Extended Type Compatibility

If Derived is a derived class of the base class Base, then you can assign an object of Derived to a variable (or parameter) of type Base, but not the other around. If you consider a concrete example, this becomes sense. For example, DiscountSale is a derived class of Sale (Displays 15.1 and 15.3). You can assign an object of the class DiscountSale to a variable of type Sale, since a DiscountSale is a Sale. However, you cannot reverse the reverse assignment, since a Sale is not necessarily a DiscountSale. The fact that you can assign an object of a derived class to a variable (or parameter) of its base class is critically important for reuse of code via inheritance. However, it does its problems.

For example, a program or unit contains the following class:

```
class Pet
{
public:
    string name;
    virtual void print() ) const;
}
class Dog : public Pet
{
public:
    string breed;
    virtual void print() ) const; //keyword virtual not needed,
//but put here for clarity.
}
```

Now concentrate on the data members, name and breed. (To keep this example simple, we have made the member variables public. In a real application, they should be private and have functions to manipulate them.)

Dog vdog;
Pet vpet;