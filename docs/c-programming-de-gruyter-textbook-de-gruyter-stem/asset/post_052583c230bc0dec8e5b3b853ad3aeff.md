
## 8.3 Virtual Function — 327

According to the type compatibility rule, we can use derived-class objects to replace base-class objects. If the base-class pointer points to a derived-class object, then we can access the object by the pointer. The problem is that we access is the member inherited from the base class. One way to solve the problem is if a base-class pointer points to a derived-class object, and we want to access a derived-class member whose name is the same as that of a base-class member, then the function in the base class should be declared a virtual function. By doing so, different objects of derived classes will have different behaviors and the execution polymorphism can be realized.

### 8.3.1 Ordinary Virtual Function

The syntax for declaring a virtual function is as follows:

```
virtual function type function name(argument list)
{
  function body
}
```

The keyword virtual is to restrict the member function in the class definition. The declaration of a virtual function can only appear in the function prototype declaration in the class definition, but not in the implementation of the member function.

Polymorphism must satisfy three conditions during execution. The first condition is having a compatible assignment rule among classes. The second one is the declaration of the virtual function, and the third is that the virtual function is called by a member function, pointer, or reference. If the virtual function is accessed by an object name, binding can be completed during compiling (static compiling), and there is no need to do it during execution.

In UML representation, an ordinary virtual function is represented by adding <<virtual>> in front of the member function.

Example 8.4: Virtual member function.

This program is a modified version of Example 7.4“compatible type rule” in Chapter 7. The member function display() is declared virtual in base class BO. There is no modification to other parts. The difference between this program and the one in Example 7.4 is that the virtual member function of the derived-class object pointed by the base-class pointer can be accessed by the base-class pointer. The derivation relation is shown in Figure 8.3 in a UML representation where class BO is a virtual function display().

```cpp
//8_4.cpp
#include <iostream>
using namespace std;
```

## 328 — 8 Polymorphism

| B0 |
| :--- |
| <<virtual>> + display() : void |
| B1 |
| + display() : void |
| D1 |
| + display() : void |

Fig. 8.3: UML of derivation relation of class B0 with a virtual function.

```cpp
//define base class B0
class B0 {
public:
    virtual void display() {cout<<"B0::display()"<<endl;}
    //virtual member function
}
class B1: public B0 //public derivation
{
public:
    void display(){cout<<"B1::display()"<<endl;}
    //virtual member function
}
class D1: public B1 //public derivation
{
public:
    void display(){cout<<"D1::display()"<<endl;}
    //virtual member function
}
void fun(B0 *ptr) //ordinary function
{
    ptr->display();
}
int main() //main()
{
    B0 b0,*ptr;//declare base-class object and pointer
    B1 b1;//declare derived-class object
}
```

```cpp
D1 d1; //declare derived-class object
p=&b0;
fun(p); //call the member function of class B0
p=&b1;
fun(p); //call the member function of derived class B1
p=&d1;
fun(p); //call the member function of derived class D1
}
```

Class BO, BI, and D1 belong to the same class family. They are derived in a public way so they satisfy the compatible type rule. At the same time, member function display() in base class BO is declared as virtual. The member function is accessed by an object pointer in the program, so the binding is completed in execution, thus implementing polymorphism. We can access the members of the pointed objects using a base-pointer, which allows objects of the same class family to be processed uniformly. The program is more succinct and efficient. The execution result of the program is as follows:

| BO::display() |
| :--- |
| B1::display() |
| D1::display() |

In the program, the derived class does not declare the virtual function explicitly. The system will follow the following rules to judge whether a derived-class member function is virtual.

- If the function has the same name as some base-class virtual function
- If the function has the same name and number of arguments and a corresponding argument type with the base-class virtual function
- If the function has the same return value or the same return value of the pointer and reference as the base-class virtual function, satisfying the assignment rule

After examining the name, arguments, and return value, the derived class is recognized as a virtual function if it satisfies all the above conditions. Here, the virtual function of the derived class overrules the virtual function of base class. And the virtual function of the derived class also hides all other forms of overloading by the function with the same name.

When the base-class constructor calls a virtual function, the derived-class virtual function will not be called. Suppose there is a base class Base and a derived class Derived. Both have the virtual function virt(). If Base::Base() calls virtual function virt(), it is Base::virt() that is called.

347

Similarly, when the base-class destructor calls a virtual function, the derived-class virtual function will not be called. Suppose there is a base class Base and a derived class Derived. Both have the virtual function virt(). If Base::~Base() calls virtual function virt(), it is Base::~virt() that is called.

In C++, one is not allowed to declare a virtual constructor, but it is legal to declare a virtual destructor.

### 8.3.2 Virtual Destructor

The syntax of a virtual destructor is as follows:

```
virtual ~name();
```

If the destructor of a class is virtual, then all classes' destructors are virtual. After setting the destructor to virtual, the pointer and reference are bound dynamically to implement polymorphism. To sum up, if it is possible to call an object's destructor by a base-class pointer (by delete), and an object to be destructed is an object of the class that has an important destructor, then the base-class destructor should be a virtual function.

Example 8.5: Example of virtual destructor.

Note that the following program does not have a virtual destructor.

```cpp
//8_5.cpp
#include <iostream>
using namespace std;
class Base
(
```

348

## 8.3 Virtual Function

public:

```cpp
~Base(){ cout<<"Base destructor\n";
};
```

```cpp
class Derived : public Base
{
public:
  Derived();
  ~Derived();
private:
  int *i_pointer;
};
```

```cpp
Derived::Derived()
{  i_pointer=new int(0); 
}
```

```cpp
Derived::~Derived()
{
  cout<<"Derived destructor\n"
  delete i_pointer;
}
```

```cpp
void fun(Base* b)
{ delete b; }
```

```cpp
int main()
{
  Base *b=new Derived();
  fun(b);
}
```

The output message during execution is:

Base destructor

This illustrates that it is the base-class destructor, rather than the derived-class destructor, which is called when deleting a derived-class object by a base-class pointer. The memory dynamically allocated derived-class objects is not freed and this causes memory leak. That is to say that the memory that i_pointer points to is not used or freed after the disappearance of the object. For a program that needs a large memory and long running time, it is dangerous to repeat the error. It may eventually cause insufficient memory error and the program will be terminated.

An effective way to avoid this error is to declare the destructor to be a virtual function:
