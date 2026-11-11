
![](img/57c0d966bb33c67a5a188e6bf39e4e02_950_0.png)

**Figure 16.1:** Size of objects o1 and o2

The statement `o1.input();` inputs two integer values a and b for object o1, whereas the statement `o1.add();` performs the addition of two integers a and b which are members of o1. Similarly, the statement `o2.input();` inputs one integer (member a) and one float (member b) for object o2, whereas the statement `o2.add();` performs the addition of member a (int type) and member b (float type) of o2.

## NOTES

The program given below creates a class with a single generic type. Under such a design, all the members of this type must be converted to the same data type for a particular instance.

```cpp
#include<iostream.h>
template<class G1> //only one generic type G1 for the class
class Data
{
private:
    G1 a;
    G1 b;
public:
    void input()
    {
        cout<<"Enter values of a and b"<<endl;
        cin>>a>>b;
    }
    void add()
    {
        cout<<"Addition of a and b is "<<a+b<<endl;
    }
};
void main()
{
    // Addition of two integers
    Data<int> o1;
    o1.input();
    o1.add();
    // Addition of two floats
    Data<float> o2;
    o2.input();
    o2.add();
}
```

### Output

```text
Enter values of a and b
10 20
Addition of a and b is 30
Enter values of a and b
11.2 33.4
Addition of a and b is 44.6
```

The statement `Data<int> o1;` creates an object `o1` specifying the generic type as `int`. This means that members `a` and `b` for object `o1` will be of type integer as shown in Figure 16.2. Whereas, the statement `Data<float> o2;` creates object `o2` specifying the generic type as `float`. This means that members `a` and `b` for object `o2` will be of type `float` as shown in Figure 16.2.

Note that under this design, it is not possible to have members `a` and `b` of different data types for the same object because we have defined just one generic type for the entire class. The generic type can take different forms for different objects, but it can take only one form for one particular object. For object `o1`, it has taken the form of `int`, whereas for object `o2`, it has taken the form of `float`.

![](img/57c0d966bb33c67a5a188e6bf39e4e02_952_0.png)

## What is the application of templates in C++?

Both function templates and class templates are used to create generic components in the program. Templates are extensively used in creating collections. Collection is a data structure used to store multiple values. For example, an array is a collection, and a linked list we created in Chapter 10 is also a collection. While creating these collections, we define a data type which informs the compiler about the type of values that the collection stores. How different is the program to create and manipulate a linked list that stores integers than the program for a linked list of floats? How different is a function that sorts an array of integers than an array of floats? Basically, everything is the same if just the keyword `int` is replaced by the keyword `float`. However, you will have to copy-paste the whole code written for `int` and create another version for `float`. And what if we wish to do it for 10 different data types? This means that you will have 10 different versions of the code. This approach will not only increase the length of the overall program but will also make it difficult to maintain. The core application of templates is to give a programmer an ability to define a generic logic and then instantiate it for different types in the program without duplicating the code. For example, we can create a program for linked list using a generic type G1 and then create individual instances of list using specific individual types. If list is the name of the generic class, then

```cpp
list<int> l1;
```

could create a linked list named l1 which can store int types only. Whereas,

```cpp
list<float> l2;
```

could create a linked list named l2 which can store float types.

The complex functions responsible to insert a node into list, delete a node from list, sort the list and so on can be easily defined using generic type within the class list, and hence they can work for objects l1 as well as l2. In practical situations, templates are widely used in creating a variety of such collections in the program to make them generic.

## 16.4 Standard Template Library: One of the Applications of Class Templates

Standard Template Library (STL) is a built-in application programming interface (API) of C++ that defines a variety of collections such as linked list, vector, map, stack, queue, and set. Programmers can use these collections directly in the program by including necessary header files. This saves programmers' efforts to create the full code for these collections in every program that needs storing data dynamically.

STL essentially defines a variety of template classes and exposes the collection classes in its API. The list of classes defined as a part of STL is as follows.

### Built-in collections in C++

You can create objects of these classes directly to use them in the program. We will explain class list in detail to help you understand the approach in which these collections can be used. The API is quite vast to actually explain each class at the same level of detail; however, going through each of the collections at the same level of detail is not required. When you understand list, you will have a clear idea of how we can use collections in general.

### 16.4.1 Linked list

The linked list API is defined in a header file `list.h`, and hence this header file must be included in the program before using the built-in list. This means that the template class `list` is defined in `list.h`.

As `list` is a template class, you can instantiate it using a generic tagged syntax as we did for other template classes. For example,

```cpp
list<int> l1;
```

creates an object `l1` of class `list` forcing the generic type to take the form of `int`. This means that `l1` is essentially a linked list that can store integers. Similarly, the statement

```cpp
list<float> l2;
```

creates linked list `l2` which can store `float` values. Needless to say, you can also create a linked list to store objects of your class. For example, if `Employee` is a class you defined and you want to store a list of employees, you can create a linked list named, say, `l3`, which can store `Employee` objects using the statement below:

```cpp
list<Employee> l3;
```

> **NOTES**
>
> The linked list we have implemented in Chapter 10 is a singly linked list in which every node has a pointer to the next node. In a linked list, you can just traverse in one direction as shown in the Figure 16.3.
>
> The built-in class `list` we are talking about is a **doubly linked list**. In this type of list, every node has a pointer to the next node as well as to the node previous to it. So each node has two pointers: one that points to the node before and the other that points to the node after. Hence, this list can be traversed in both the directions **forward** (from first node to the last node) as well as **reverse** (from last node to the first node) as shown in Figure 16.4.

![](img/57c0d966bb33c67a5a188e6bf39e4e02_954_0.png)

![](img/57c0d966bb33c67a5a188e6bf39e4e02_954_1.png)

The design of doubly linked list is complex compared to singly linked list, but it has an advantage that you have an option to go back and forth from any random node. Anyway, we are not really creating a program to implement doubly linked list, it is already present in the header file `list.h`. We are just users of the `list`, and we will use it to store values. This is a very good example of abstraction offered by the API; we really don't care how the list is internally implemented; all we should know is how to use the linked list. Out of interest, readers can go through the header file `list.h` to see the full source code of doubly linked list, but it is not needed at this stage. In this section, we explain how to use the built-in `list` class of STL.

### Create and traverse a list

The following program creates a linked list to store `int` values, inserts elements in the linked list, and then traverses the list in forward direction. We will understand this program step by step.

```cpp
#include<list.h>
void main()
{
    list<int> l1;
    int i;
    for(i=0;i<=10;i++)
```
