
![](img/57c0d966bb33c67a5a188e6bf39e4e02_683_0.png)

**Figure 12.15:** Constructor with two arguments invoked for P3

of P3, as seen in the code. The complete process to perform addition of Point objects is exactly the same as discussed in Chapter 11. Therefore, x value of P3 will be 20 and y value of P3 will be set to 30 after the execution of the `add()` function as shown in the Figure 12.16.

![](img/57c0d966bb33c67a5a188e6bf39e4e02_683_1.png)

**Figure 12.16:** Addition of objects P1 and P2 performed by function `add()`

> **What is the significance of an empty constructor that takes no parameters inside class Point?**
>
> When we do not write a constructor in the class, the compiler still provides a default constructor for every class, so as to create objects of that class. The constructor provided by the compiler does not take any arguments. However, the compiler will not provide any default constructor to the class if the programmer defines a constructor with parameters. In this case, we have created a constructor with parameters inside class Point and hence the compiler will not provide any default constructor to class Point. This means that statement:
>
> ```cpp
> Point P3;
> ```
>
> will not work because, in this case, a default constructor is to be invoked for creating object P3. Hence, we have created an empty constructor without any parameters so as to allow the creation of the objects of class Point without passing any parameters. Therefore, we can now create object P3 successfully.

## 12.5 Constructor with Default Arguments

You can specify default values to the parameters of the constructor. The rules for creating constructors with default arguments are the same as those for creating functions with default arguments as specified in Chapter 7, Section 7.11. For example, consider a Point constructor as written below:

```cpp
Point(int a, int b = 20)
{
    x = a;
    y = b;
}
```

This constructor has two parameters a and b. The value of parameter b is defaulted to 20, which means that if the value of b is not passed by the caller, it will be considered as 20. In summary, the constructor is coded such that it is mandatory to pass the value of the first parameter, whereas specifying the value of the second parameter is optional.

```cpp
Point p1(10);
```

will initialize the first parameter of the constructor to 10, whereas the default value is used for the second parameter. Hence, this statement will create an object p1 with x value initialized as 10 and y value initialized as 20. However, you could also create a point object as

```cpp
Point p2(100, 200);
```

While creating p2, we have specified both the values. Hence, it also calls the same constructor, with the only difference being the default value of parameter b will not be used this time. This statement creates a point object p2 with value of x as 100 and value of y as 200.

## 12.6 Cloning Objects using Constructor/Copy Constructor

A constructor that takes the reference to the object of the same class as an argument to copy the values of the member variables of one object into another object is called a ‘copy constructor’. For example, let us create a class Data with members a and b of type integer and float, respectively. We have written three constructors in class Data as shown in the Figure 12.17.

![](img/57c0d966bb33c67a5a188e6bf39e4e02_684_0.png)

```cpp
class Data
{
private:
    int a;
    float b;

public:
    Data()
    {
        a = 0;
        b = 0;
    }

    Data(int p, float q)
    {
        a = p;
        b = q;
    }

    Data(Data& t)
    {
        a = t.a;
        b = t.b;
    }
    ......
};
```

The first constructor is the constructor without parameters, and the second constructor is the constructor with two parameters as shown in the Figure 12.17. The third constructor takes reference to another object of class Data as an argument, thereby copying the member values of some other object into the object that is to be created by the constructor.

The following is the source code that illustrates the usage of the copy constructor.

```cpp
#include<iostream.h>
class Data
{
private:
    int a;
    float b;
public:
    Data()
    {
        a = 0;
        b = 0;
    }
    Data(int p, float q)
    {
        a = p;
        b = q;
    }
    Data(Data& t)
    {
        a = t.a;
        b = t.b;
    }
    void output()
    {
        cout << "a= " << a << " b= " << b << endl;
    }
};
void main()
{
    Data d1(10, 2.5);
    Data d2(d1);
    Data d3;
    Data d4(d3);
    cout << "-------------d1----------------" << endl;
    d1.output();
    cout << "-------------d2----------------" << endl;
    d2.output();
    cout << "-------------d3----------------" << endl;
    d3.output();
    cout << "-------------d4-------------" << endl;
    d4.output();
}
```

### Output

![](img/57c0d966bb33c67a5a188e6bf39e4e02_686_0.png)

Let us trace the output of the code from the first line of the main() function. The statement

```cpp
Data d1(10, 2.5);
```

creates an object d1 of class Data by invoking the constructor with two arguments, thereby initializing the members a and b to 10 and 2.5, respectively, as shown in the Figure 12.18. The next statement

```cpp
Data d2(d1);
```

creates the object d2 of class Data by invoking a 'copy constructor' with passing the object d1 as an argument to the constructor. As seen, the object d1 is passed by reference, therefore the reference variable t (which is created as a formal argument to the constructor) now represents another name to the actual argument d1. Hence, we can now access the value of the member a of object d1 as t.a and the value of the member b of object d1 as t.b. This is because the reference t is just another name to object d1. Also, it is important to understand that the copy constructor is invoked for the object d2, and hence the members a and b of object d2 can be directly accessed inside the copy constructor as seen in the Figure 12.19. Therefore, the copy constructor will copy the members of object d1 into object d2, using a reference variable t as shown in the Figure 12.19. Hence, the values of the members a and b of the object d2 will also be 10 and 2.5 respectively, which are exactly the same as those of the object d1.

![](img/57c0d966bb33c67a5a188e6bf39e4e02_686_1.png)

**Figure 12.18:** State of object d1

![](img/57c0d966bb33c67a5a188e6bf39e4e02_688_0.png)

**Figure 12.21:** Invoking the copy constructor for object d4

To understand the usage of copy constructors, let us understand the description of three C++ statements tabulated below:

| C++ Statement | Description |
|---|---|
| `Data d2(d1);` | The statement will invoke a copy constructor defined inside class Data. Hence, the member values of the object d1 will be copied into object d2 by the copy constructor defined in class Data. |
| `Data d2=d1;` | As seen, we have applied an initialization operator with the objects d2 and d1 at the time of creating the object d2. As the assignment is performed at the time of creation of the object d2, this statement is exactly the same as that of the previous statement `Data d2(d1);`. Hence, the statement `Data d2=d1;` will invoke a copy constructor for object d2 by passing object d1 as an argument. Hence, the member values of the object d1 will be copied into object d2 by the copy constructor defined in class Data. |
| `Data d3;`<br>`d3=d2;` | The first statement creates an object d3 of class Data, thereby invoking a default constructor for d3. This is because we have not passed any parameters while creating the object d3. Hence, the members a and b of object d3 will be set to **zero** by the default constructor. Now, the second statement `d3=d2;` will perform a member-by-member initialization of the object d3 from the object d2. It is important to note that the statement will not invoke a copy constructor as the assignment among the objects is not applied at the time of creation of the object d3. Although, as an effect of this statement, the members a and b of object d3 will be initialized with the values of members a and b of object d2, the key point to note here is that the copy constructor will not be invoked to execute this statement. |

## 12.7 Allocating Dynamic Memory Inside Constructor

A constructor that allocates dynamic memory is called a dynamic constructor. We recollect from Chapter 10 that C++ supports an operator new for dynamic memory allocation. This means that when we use the keyword new or any other function that dynamically allocates memory inside a constructor, such a constructor is called a dynamic constructor. This is because the constructor will then allocate memory to the members of the objects at runtime of the program.

As an example to understand dynamic constructors, let us create a class ArrayList that can be used to create an integer array at runtime of the program. This means that we will create a constructor in the class ArrayList, which will dynamically create an array of the required size. Hence, the programmer can pass the capacity of the array list to be created as an argument to the constructor following which the constructor can create an array using the new operator as seen in the code.

Also, we will create the following functions to perform operations with the array list.

- 1. `void add(int);` The function `add()` will insert an integer element into the array list which is passed to it as an argument.
- 2. `int getCapacity();` The function returns the maximum capacity of the array list.
- 3. `void display();` The function can be used to print all the elements of the ArrayList on the computer screen.

Also, we will create a copy constructor to perform copy operation from one ArrayList object to another. For example, the following statement:

```cpp
ArrayList L2(L1);
```

will create an array list named as L2, which is the exact copy of the existing array list L1.

Along with the above member functions, the class ArrayList also contains the following members as listed below:

- 1. **Integer type pointer p:** The pointer p points to the dynamically created array to which the programmer can add elements.
- 2. **Integer variable count:** The variable count represents the total number of elements currently stored in the array list. The initial value of the variable count will be set
