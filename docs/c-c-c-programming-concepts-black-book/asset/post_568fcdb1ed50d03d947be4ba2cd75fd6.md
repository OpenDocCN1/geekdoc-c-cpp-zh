
```cpp
#define MAX 100
Geometry *ptr[MAX];

for (int i = 0; i < MAX; i++) {
    ptr[i]->calculateArea();
}
```

In the preceding code snippet, we have put all the object pointers of the derived classes in the array ptr, loop over the number of objects using MAX, and called the calculateArea() function of each object. Therefore, completely different functions are being executed by the same function call. For example, if ptr points to a triangle object, then it calculates the area for a triangle. Similarly, if ptr points to a pentagon object, then it calculates the area for a pentagon. This is also a form of polymorphism.

Let's learn more about virtual functions and polymorphism.

## Virtual Functions and Polymorphism – Early Binding and Late Binding

As already learned, C++ supports polymorphism at both compile time and runtime. Compile time polymorphism is achieved through function overloading and operator overloading and runtime polymorphism is achieved through inheritance and virtual functions. Associated with compile time polymorphism and runtime polymorphism is the concept of early binding and late binding.

Early binding or static binding refers to the events that occur at compile time. In essence, early binding means that all the information required to call a function is available and known at compile time. This implies that the object and the function calls are bound during compile time. Examples of early binding include normal calls to functions, overloaded functions, and overloaded operator functions. The main advantage of early binding is efficiency. As all the information needed to call a function is available at compile time, function calls are executed very fast.

The opposite of early binding is late or dynamic binding. With reference to C++, late binding refers to the function calls that are not resolved until runtime. Virtual functions are used to achieve runtime polymorphism or late binding. As learned already, when access to the object's members is done through a base class pointer, figuring out the actual function to be called is delayed till runtime depending on the type of object pointed to by the pointer. As this cannot be determined at compile time, the object and the function are not linked until runtime. The main advantage of late binding is flexibility. Unlike early binding, late binding allows us to create programs that can respond to events that occur while the program executes. One thing we should keep in mind that in case of late binding, late binding can make somewhat slower execution, as the function call is not resolved until runtime.

In the next section, let's discuss about the calling mechanism of virtual functions.

### Calling Mechanism of Virtual Functions

Let's now see what happens if we do not use virtual functions and still try to achieve runtime polymorphism in our program. For this, we first write a program without using virtual functions:

```cpp
1:/* Virtual Function Example Program 1 */
2:#include <iostream.h>
3:using namespace std;
4:
5:class Base {
6:public:
7:void show ()
8:{
9:    cout<<"Inside class Base"<<endl;
10:    }
11:};
12:
13:class Derived1 : public Base {
14:public:
15:    void show ()
16:    {
17:        cout<<"Inside class Derived1"<<endl;
18:    }
19:};
20:
21:class Derived2 : public Base {
22:public:
23:    void show ()
24:    {
25:        cout<<"Inside class Derived2"<<endl;
26:    }
27:};
28:
29:int main()
30:{
31:    Derived1    deriv1_Obj;    /* Object of Derived1   */
32:    Derived2    deriv2_Obj;    /* Object of Derived2   */
33:    Base  *ptr;              /* Pointer to Base Class */
34:
35:    ptr = &deriv1_Obj;       /* Putting addr of deriv1_Obj in ptr */
36:    ptr->show();             /* Trying to call Derived1's show() */
37:
38:    ptr = &deriv2_Obj;       /* Putting addr of deriv2_Obj in ptr */
39:    ptr->show();             /* Trying to call Derived2's show() */
40:
41:    return 0;
42:}
```

In the preceding code, the Derived1 and Derived2 classes are derived from the Base class. Each of these three classes has a member function, named show(). In the main() function, we have created objects of both the derived classes and defined a pointer to the Base class. In line number 35, we have tried to put the address of a derived class object into the base class pointer. The compiler does not raise any error about this operation because pointers to objects of a derived class are *type-compatible* with pointers to objects of the base class. Now, the question arises that which function is called when we execute line number 36? Is it the Base::show() function or the Derived1::show() function? Similar operation is also tried with the object of Derived2. Let's see the answer to this question by executing the program. The output of the program is as follows:

```
Inside class Base
Inside class Base
```

As we can see, the function in the base class is always executed. The compiler completely ignores the content of *ptr* and chooses the member function that matches the type of the pointer. Therefore, our objective of achieving runtime polymorphism in C++ could not be done using the preceding code. Let's now incorporate virtual functions into the preceding program to see the changes in the output:

```cpp
1:/* Virtual Function Example Program 2 */
2:#include <iostream.h>
3:using namespace std;
4:
5:class Base {
6:public:
7:    virtual void show ()      /* Virtual Function */
8:    {
9:        cout<<"Inside class Base"<<endl;
10:    }
```

> **NOTE**
> 
> *A class that includes a virtual function is called a polymorphic class.*

### Base and Derived Virtual Functions

When a virtual function is inherited, its virtual nature is also inherited. This implies that when a derived class inherits a virtual function from a base class and another class is created by deriving the derived class, the original virtual function of the base class can be overridden. Let’s write the following program to demonstrate the concept:

```cpp
/* Virtual Function Example Program 3 */
#include <iostream.h>
using namespace std;

class Base {
public:
    virtual void show ()        /* Virtual Function */
    {
        cout<<"Inside class Base"<<endl;
    }
};

class Derived1 : public Base {
public:
    void show ()
    {
        cout<<"Inside class Derived1"<<endl;
    }
};

class Derived2 : public Derived1 {
public:
    void show ()                 /* This is still virtual */
    {
        cout<<"Inside class Derived2"<<endl;
    }
};

int main()
{
    Derived1      derv1_obj;    /* Object of Derived1     */
    Derived2      derv2_obj;    /* Object of Derived2     */
    Base *ptr;                   /* Pointer to Base Class  */

    ptr = &derv1_obj;            /* Putting addr of derv1_obj in ptr */
    ptr->show();                 /* Trying to call Derived1's show() */

    ptr = &derv2_obj;            /* Putting addr of derv2_obj in ptr */
    ptr->show();                 /* Trying to call Derived2's show() */

    return 0;
}
```

### Polymorphism and Inheritance

In the preceding program, we have defined a Base class that contains a virtual show() function. In addition, we have defined the Derived1 class, which is derived from the Base class, overriding the show() function. Now, what happens when we define another class called Derived2 by deriving the Derived1 class? The following output provides the answer:

```
Inside class Derived1
Inside class Derived2
```

In both the cases, the virtual function of the Base class is overridden.

As already learned, when a function is declared as virtual by a base class, a derived class may override it. However, if a derived class does not need to override a virtual function, then when an object of that class accesses the function, the function defined by the base class is used. The following program illustrates what happens when a derived class fails to override a virtual function:

```cpp
/* Virtual Function Example Program 4 */
#include <iostream>
using namespace std;

class Base {
public:
    virtual void show ()        /* virtual Function */
    {
        cout<<"Inside class Base"<<endl;
    }
};

class Derived1 : public Base {
public:
    void show ()
    {
        cout<<"Inside class Derived1"<<endl;
    }
};

class Derived2 : public Base {
};

int main()
{
    Derived1    derv1_obj;      /* Object of Derived1 */
    Derived2    derv2_obj;      /* Object of Derived2 */
    Base *ptr;                   /* Pointer to Base Class */

    ptr = &derv1_obj;            /* Putting addr of derv1_obj in ptr */
    ptr->show();                 /* Trying to call Derived1's show() */

    ptr = &derv2_obj;            /* Putting addr of derv2_obj in ptr */
    ptr->show();

    return 0;
}
```

In the preceding program, we have omitted the show() function in the Derived2 class. Following is the output of the program:

```
Inside class Derived1
Inside class Base
```
