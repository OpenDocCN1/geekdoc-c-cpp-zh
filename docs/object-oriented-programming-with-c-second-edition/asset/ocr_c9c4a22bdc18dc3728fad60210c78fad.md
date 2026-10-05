# Listing 5.27 Ambiguity resolution by using scope resolution operator

```
/*Beginning of multiInheritAmbiguityResolve01.cpp*/
void<iostream.h>
Class A
{
    Public:
    void show()
    {
        cout<<"show() function of clas A called\n";
    }
}
class B
{
    Public:
    void show()
    {
        cout<<"show() function of class B called\n"\n    }
}
class C : public A, public B
{
    void main()
    {
        C1;
        C1.A::show();            //OK: show() function of class A called
        C1.B::show();            //OK: show() function of class B called
    }
}
/*End of multiInheritAmbiguityResolve01.cpp*/
```

Output
show() function of class A called
show() function of class B called

This ambiguity can also be resolved by overriding the multiple inherited base class member as shown in Listing 5.28.

# Listing 5.28 Ambiguity resolution by overriding

```
/*Beginning of multiInheritAmbiguityResolve02.cpp*/
#include<iostream.h>
class A
{
    public:
    void show()
    {
        cout<<"show() function of class A called\n"
    }
}
class B
{
    public:
    void show()
```