```
```cpp
Ptrobj = new C;
Ptrobj->display1();
Ptrobj->A::display2();
return 0;
}
```
```

# **Output:**

```
```text
class B: Function display 1
class A: Function display 2
class C: Function display 1
class A: Function display 2
```
```

In Listing 38, class A has two virtual functions, display1() and display2(). The virtual function, display1(), is overridden by the derived classes, B and C, as both classes have their own display1() function. However, the display2() virtual function is overridden by the C derived class only.

Now, in the main() function, the PtrObj object of class A is created, which points out to the B class. The PtrObj object invokes the display1() function of class B and the display2() function of class A. This is because class B does not have the definition of the display2() function of its own. Next, the PtrObj object points out to the C class, then it invokes the display1() function of the C class and the display2() function of the A class, though the C class has its own display2() function. This is because the pointer object invokes the display2() function of class A explicitly by using the :: operator.

# ## TEST YOUR KNOWLEDGE

Q9. Create a base class called Shape, which contains the methods to calculate the area of various figures. Now, derive two classes, namely Rectangle and Triangle, from the Shape class and override the base class (Shape) methods in these classes to accept the values for the sides of the shape and then calculate the area of that shape (Hint: use the concept of virtual functions).

Ans.

```
```cpp
#include<iostream.h>

class Shape
{
    protected:
        double arearect;
        double areatri;
        int x,y;
    public:
        virtual void get_data()
        {
            arearect=0;areatri=0;x=0;y=0;
        }
}
```
```