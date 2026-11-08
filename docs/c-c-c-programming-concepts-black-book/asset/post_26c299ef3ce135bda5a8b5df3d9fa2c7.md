

```cpp
    {
        c = val + (a*b);      /* valid access to a and b */
    }
    int showDerv1()
    {
        cout<<"c = "<<c<<endl;
    }
};

class Derived2 : public Derived1 {
    int d;
public:
    void setDerv2(int val)
    {
        d = val + a + b;      /* valid access to a and b */
    }
    int showDerv2()
    {
        cout<<d<<endl;
    }
};

int main()
{
    Derived1    Derv1_obj;
    Derived2    Derv2_obj;

    Derv1_obj.set(2,3);
    Derv1_obj.show();
    Derv1_obj.setDerv1(5);
    Derv1_obj.showDerv1();

    Derv2_obj.set(3,4);
    Derv2_obj.show();
    Derv2_obj.setDerv1(8);
    Derv2_obj.showDerv1();
    Derv2_obj.setDerv2(10);
    Derv2_obj.showDerv2();

    return 0;
}
```

In the preceding program, the Base class has two protected members: a and b. Now, both the derived classes, Derived1 (directly inherited from the Base class) and Derived2 (inherited from the Derived1 class), has a copy of the protected members 'a' and 'b' of the Base class as protected in their class space. On the other hand, Derived1 has a private member 'c'. When Derived2 inherits Derived1 with public access, it will result in an error if an object of the Derived2 class attempts to access 'c' directly. However, if the Base class were inherited as private, then all the members of the Base class would become private members of the Derived1 class. This implies that the members of the Base class would not be accessible by Derived2, although 'a' and 'b' would still be accessible by Derived1. The output of the preceding program is as follows:

```
a = 2 b = 3
c = 11              /* It is calculated as 5 + (2*3) */
a = 3 b = 4
c = 20              /* It is calculated as 8 + (3*4) */
d = 17              /* It is calculated as 10 + 3 + 4 */
```

Let's now learn about multiple inheritance.

```cpp
int main()
{
    Derived       obj;

    obj.set(2,3);
    obj.showBase1();
    obj.showBase2();

    return 0;
}
```

In the preceding program, the Derived class inherits from both the base classes, Base1 and Base2. The protected and public members of the base classes became the protected and public members of the Derived class itself. Derived class contains not only its own member functions, but also the data members and member functions of the Base1 and Base2 classes.

Following is the output of the preceding program:

```
a = 2
b = 3
```

Now, consider a situation where a derived class is inheriting from two or more classes and any two of them have functions with the same name. In this case, if the object of a derived class invokes a function by name, then it gives rise to ambiguity. Therefore, before finishing this topic, let's discuss about various ambiguities in multiple inheritance.

## Ambiguities in Multiple Inheritance

While programming, we can encounter different types of problems. Let's consider a situation where two base classes have member functions with the same name, while a class derived from these two base classes does not have any function with the same name. Then, how do objects of the derived class access the correct base class function? In this case, only function name is insufficient, since the compiler cannot figure out to which version we are actually calling. Therefore, let's write the following program to solve the ambiguity:

```cpp
/* Inheritance Example Program */
#include <iostream.h>
using namespace std;

class Base1 {
public:
void show ()
{
    cout<<"Inside class Base1"<<endl;
}
};

class Base2 {
public:
        void show ()
        {
            cout<<"Inside class Base2"<<endl;
        }
};

class Derived : public Base1, public Base2 {
};

int main()
{
    Derived       Obj;

    //Obj.show();        /* Ambiguous - will not compile */
    Obj.Base1::show();  /* works */
    Obj.Base2::show();  /* works */

    return 0;
}
```

As shown in the preceding program, the ambiguity can be resolved through scope resolution operator by specifying the class name in which the function lies. Therefore, the following statement refers to the version of the show() function in the Base1 class:

```cpp
Obj.Base1::show();
```

Similarly, the following statement refers to the version of the show() function in the Base2 class:

```cpp
Obj.Base2::show();
```

Note that in the preceding program, we have commented line number 38 intentionally. If the line number 38 is uncommented, then the program will result in compilation error due to the ambiguity associated with the statement. This is because the object of the Derived class does not have any knowledge as to which version of show() should be executed. Therefore, we have used the scope resolution operator as a solution.

Another kind of ambiguity may occur if we derive a class from two classes, which in turn are derived from a single class. This creates a diamond-shaped inheritance structure. Let's write the following program to understand more about the ambiguity:

```cpp
#include <iostream.h>
using namespace std;


class A {
public:
 void show ()
{
 cout<<"Inside class A"<<endl;
       }
};

class B : public A {
};

class C : public A {
};

class D : public B, public C {
};

int main()
{
       D       Obj;

       Obj.show();        /* Ambiguous - will not compile */

       return 0;
}
```

In the preceding program, B and C classes are both derived from the A class, and the D class is derived by multiple inheritance from both B and C. Trouble starts when we try to access a function show() in A from an object of D. In the program, the obj object of D tries to access show(). However, as both B and C contains a copy of the show() function, inherited from A, the compiler cannot decide which copy to use and finally raises an error. To handle this ambiguity, we can apply the scope resolution operator to show() and select any of the derived class's copy of show(). Let's rewrite the same program with scope resolution operator to remove this ambiguity:

```cpp
/* Inheritance Example Program 10 */
#include <iostream.h>
using namespace std;

class A {
public:
void show ()
{
 cout<<"Inside class A"<<endl;
 }
};

class B : public A {
};

class C : public A {
};

class D : public B, public C {
};

int main()
{
 D Obj;

 Obj.A::show(); /* Unambiguous - will compile */

 return 0;
}
```

In line number 26, we are using the scope resolution operator to remove the ambiguity associated with the multiple inheritance. On using the '::' operator, the program manually selects the class A version of the function to be executed. However, what if we require only a single copy of the base class A. In other words, is there any way to prevent two copies from being included in the D class? The answer to all these queries is virtual base classes. Let's now learn about them in the next section.

## Virtual Base Classes

When two or more subclasses (say, B and C) are derived from a common base class (say, A) and a third class (say, D) is generated by inheriting these subclasses, we can prevent multiple copies of the base class from being present in the object of D by declaring the base class as virtual when it is inherited. This can be done by attaching the keyword virtual before the base class name. Let's write the following program to see how virtual base classes work:

```cpp
/* Inheritance Example Program 11 */
#include <iostream.h>
using namespace std;

class A {
public:
void show ()
{
    cout<<"Inside class A"<<endl;
}
};

class B : virtual public A {
};

class C : virtual public A {
};

class D : public B, public C {
};

int main()
{
   D    obj;

   obj.show();           /* Unambiguous - will compile */

   return 0;
}
```

In the preceding program, the keyword virtual precede the access specification of the inherited class. Now that both the B and C classes have inherited the base class A as **virtual**, any multiple inheritance involving them will cause only one copy of show() to be present. Therefore, in the D class, there will be only one copy of show(), making it a valid and unambiguous access.

Note that even though both the B class and the C class inherit the base class A as virtual, still show() will be present in both the subclasses. The only difference between a normal base class and a virtual one is that an object can inherit the base class more than once. If virtual base classes are used, then only one base class member will be present in the object making it unambiguous; otherwise, multiple copies will be found.

Let's now learn about virtual functions.

## Virtual Functions

Virtual means existing in appearance but not in reality. When virtual functions are used, a program that appears to be calling a function of one class, may in reality calling a function of a different class. A *virtual function* is a function that is declared as **virtual** in a base class and redefined by a derived class. To declare a function as virtual, its declaration should be preceded by the keyword **virtual**. The redefinition of the function in the derived class overrides the definition of the function in the base class. A virtual function declared in the base class acts as a placeholder that specifies a general class of actions and stipulates the form of the interface. It is basically the redefinition of the virtual function, by the derived class, that performs the actual operation. Then why do we need virtual functions?

Consider a situation where we have a number of objects of different classes and we want to put all of them into an array and perform a particular operation on them by calling a specific function. Suppose we have a base class *Geometry*. Let's now make one class per geometrical figure, such as *triangle*, *square*, *rectangle*, *circle*, and *pentagon*. All these classes will inherit from the base class Geometry. Now to keep the objects of these classes in an array, we need to write the following code snippet:

