
Hence, to solve this problem, we must create `f1()` as a virtual function, which means that the statement

```cpp
p->f1();
```

will invoke the function in the correct class whose object is pointed by the pointer `p`.

To create a function as virtual, keyword `virtual` must be added to the function defined in parent class. There is no need to specify keyword virtual in each of the child classes which override the function. Figure 14.52 gives the syntax of creating `f1()` as a virtual function.

![](img/57c0d966bb33c67a5a188e6bf39e4e02_850_0.png)

**Figure 14.52:** Syntax of creating virtual functions

The following are rules for creating virtual functions:

- 1. A function can be created as virtual only if it is present in parent class. If the function is present only in child class but not in parent, then you cannot make the function as virtual.
- 2. A child class may or may not override the virtual function defined by parent class. If the child class overrides the virtual function defined in parent, C++ guarantees that the function defined in correct child class will be called, when invoked using a pointer pointing to child object.
- 3. If the child class does not override the virtual function defined by parent, the function defined in parent class will be called when invoked by a pointer pointing to a child object.
- 4. It makes sense to create a function as virtual only if it’s overridden by at least one child class. If the function is only defined in parent class and no child overrides it, then it means that every child is interested in using same implementation as that of the parent and function of parent class must be invoked in all cases even if the pointer points to child. This is the default behaviour of early binding anyways; and hence there is no need to create virtual functions in this case.

As an example of virtual functions, let us consider the hierarchy as shown in the Figure 14.53:

![](img/57c0d966bb33c67a5a188e6bf39e4e02_851_0.png)

**Figure 14.53:** An example of virtual function

The function `output()` of class Person (parent) is overridden by both the child classes Student and Professor, hence we can create `output()` as a virtual function. The function `inputP()` is defined only in parent class Person and not overridden by any child, hence it does not make any sense to create it as virtual as per Rule 4. The functions `inputS()` or `inputPr()` are specialized functions in each of the child classes and they are not present in parent class Person. Therefore, you cannot make these functions as virtual as per Rule 1.

The following is the complete source code creating `output()` as a virtual function:

```cpp
#include<iostream.h>
class Person
{
protected:
    int id;
    char name[100];
public:
    void inputP()
    {
        cin>>id>>name;
    }
    virtual void output()
    {
        cout<<id<<" "<<name<<endl;
    }
};
class Student: public Person
{
private:
    int marks;
public:
```

```
p->output();
}
Enter id and name of Person
1 John
Person details are
1 John
Enter id, name and marks of Student
2 Jack 90
Student details are
2 Jack 90
Enter id, name and salary of Professor
3 Jill 5000
Professor details are
3 Jill 5000
```

The first three statements of `main()` function

```cpp
Person p1;
Student s1;
Professor prof1;
```

create objects of class Person, Student, and Professor respectively, as shown in the Figure 14.54.

![](img/57c0d966bb33c67a5a188e6bf39e4e02_853_0.png)

We create a pointer of type Person (parent type) in the program, using the statement below:

```cpp
Person *p;
```

We can make the pointer p to point to parent object or to any of the child objects.

The statement

```cpp
p=&p1;
```

makes the pointer p to point to Person (parent) object p1. There has to be no confusion at this stage because the type of the pointer is same as the type of the object to which it points to. Hence the statements

```cpp
p->inputP();
```

and

```cpp
p->output();
```

invoke the `inputP()` and `output()` functions defined in class Person. It is still important to technically differentiate between the two calls: `inputP()` is not a virtual function and hence early binding will be performed for resolving its call, whereas `output()` is a virtual function and hence late binding will be performed for resolving its call. In this case, since the data type of pointer and object is exactly same, it really doesn’t matter to us as to which type of binding internally happens but C++ will always perform late binding for virtual functions. Assuming the sample input as `id=1` and `name=John`, Figure 14.55 shows the state of object p1 and a pointer p pointing to it.

![](img/57c0d966bb33c67a5a188e6bf39e4e02_854_0.png)

The statement

```cpp
p=&s1;
```

makes the pointer p point to a Student object s1 as shown in the Figure 14.56. Object of class Student has three members and we need to invoke the function `inputS()` to accept all the three values as input from the user. We have mentioned before that `inputS()` is not (and cannot be) created as a virtual function because it is only defined in the child class. Hence the only option to invoke it using a parent pointer p is by **explicitly down casting** the pointer to Student* as discussed in section 14.10. This is as seen in the statement

```cpp
((Student*)p)->inputS();
```

Assuming the sample input values as `id=2`, `name=Jack`, and `marks=90` the state of Student object s1 will be as shown in the Figure 14.56.

![](img/57c0d966bb33c67a5a188e6bf39e4e02_854_1.png)

The statement

```cpp
p->output();
```

will invoke the `output()` function defined in class Student. This is because the function `output()` is a virtual function, and the decision on which `output()` function to call is taken based on the type of the object pointed by p and not based on the type of p; as per the principle of late binding. Therefore, the statement correctly invokes the `output()` function of class Student because p points to the object of type Student. This will print the values id, name, and marks of object s1 on the computer screen.

Similarly, when p points to the Professor object, the statement

```cpp
p->output();
```

will correctly invoke the `output()` function inside class Professor using late binding.

## NOTES

Binding is a process to attach a function call with the function definition. We have discussed **early binding** in Chapter 11 Section 11.2.5. In this section, we have explained another type of binding called as **late binding** which is performed only for virtual functions. Given below is the comparison of these two types of bindings performed by C++ in different scenarios and at different times

| Early binding | Late binding |
|---|---|
| This is the binding performed at compile time of the program. This is also called as static binding or compile time binding | This is the binding performed at run time of the program. This is also called as dynamic binding or run time binding |
| This type of binding is performed in following cases of polymorphism<br>1. Function overloading<br>2. Operator overloading<br>3. Constructor overloading | This type of binding is performed for virtual functions only |
| This is a basic binding performed by the compiler to resolve any of the function calls made to non-virtual functions | |
| If p is the pointer invoking the function, then the decision about which function to call is taken based on the data type of p and is immaterial of the data type of the target object to which p points to. | If p is the pointer invoking the function, the decision about which function to call is taken based on the type of target object to which p points to. |
| This type of binding is used to implement compile time polymorphism in the program | This type of binding is used to implement run time polymorphism in the program |

## NOTES

When a virtual function defined in parent class has a return type R, then the return type of the function overridden in child class must be either R or a child of R.

For example, the following overriding of virtual function will give an error because the return type of `output()` defined in parent class P is `int` and it does not match with the return type of `output()` defined in child class C which is `float`.

```cpp
class Abc
{
public:
        virtual int output() //returns int
        {
```
