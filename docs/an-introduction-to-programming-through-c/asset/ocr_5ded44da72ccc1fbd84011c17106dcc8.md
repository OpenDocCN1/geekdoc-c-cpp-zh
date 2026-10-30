statements use aptr. In the first, we access the member x, using the standard syntax aptr->x, and this will print 2 as expected. In the next statement, aptr->f(), we have invoked the member function f. Here there is some possible confusion: will this mean the f defined in A or the f defined in B? The default answer is that since aptr is of type pointer to A, the members from A will be used. Thus, this will print the message "Calling f of A.". If you are unhappy with this default, hold on till Section 23.3.

Note that in the above code, we cannot assign an object of the superclass into a variable of the subclass, i.e. write b = a;. The intuition behind this, going to our flower example, is as follows. Wherever a flower is expected, you can supply a rose; however, if a rose is expected, you cannot supply an arbitrary flower. Likewise, it is incorrect to write bptr = &a as well.

Finally, we can create references of the type superclass to objects of the subclass. This is done at the end of Figure 23.3. Indeed even in this case the function f in A will be invoked.

# 23.3 Polymorphism and virtual functions

Consider the code of Figure 23.3. As we discussed above, the call aptr->f() will cause the function f in class A to be used. But you might say: aptr really points to an object of type B so isn’t it more useful if the f in B were used? You can make this happen by declaring f to be a virtual function. For this, you simply add the keyword virtual before the definition of f in A. Thus the definition of A would have to be:

```
class A{
public:
    int x;
    A(){ x = 1; }
    virtual void f(){cout <<"Calling f of A.\n";}
};
```

The keyword virtual says that the definition of f should not be treated as a unique, final definition. It is possible that f might be over-ridden in a subclass, and if so, that definition of f which is most appropriate (most derived!) for the object on which the call is made should be considered. When we call aptr->f(), the most appropriate definition for f is the one in B, since aptr actually points to an object of type B. So that definition gets used, and our code will now indeed print "Calling f of B.".

Note further that if f is virtual, its most derived version will get used if it is invoked on a reference as well. Thus the last statement of Figure 23.3 will also cause f from B to be invoked.

Here is a more subtle example of the same idea.

```
class Flower{
public:
    void whoAmI(){ cout << name() << endl; }
    virtual string name(){ return "Flower"; }
};
```