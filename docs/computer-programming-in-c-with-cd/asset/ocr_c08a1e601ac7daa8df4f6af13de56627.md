# 4.3 Using Pointers as Function Arguments

A function is a set of statements that has a name and used for performing specific action at run time. Functions can also take arguments that are essential to call the function from any other part of the program. We have already discussed functions in Chapter- 3, *Working with Arrays and Functions*. In C++, we can use pointers as function arguments. The main objective of passing pointers as function arguments is to reflect the changes made on a variable inside a function body from where the function is called. Using pointer as function arguments is known as the call-by-reference method. This is in contrast with the call-by-value method where any changes made on the data inside the function body are not reflected outside the function body. Listing 12 shows a program that passes pointer as function argument (you can find the `PointerArgument.cpp` file on the CD in the `code\chapter4` folder):

# ▶ Listing 12: Passing Variable by Reference Using Pointer

```
```cpp
#include<iostream.h>

void add(int *p1);//function prototype declaration
int main()
{
    int n1=10;
    cout<<"Initial value of n1 is "<<n1<<endl;// value before function call
    add(&n1);//calling function with arguments matching the pointer variables
    cout<<"Value of n1 after adding 5 is: "<<n1<<endl;

    return 0;
}

void add(int *p1)
{
    *p1=*p1+5;//change the value at the address passed
}

Output:

Initial value of n1 is 10
Value of n1 after adding 5 is: 15
```
```

In Listing 12, our main purpose is to pass the pointer variable as the function arguments. Initially, we are declaring an integer variable `n1`. Now, we pass the address of this variable by using `&` operator. Inside the function body, we change the value of `n1` at the address referenced by the pointer variable `*p1` by 5. After calling the `add()` function, the value of `n1` is changed by using pointer and the changed value gets printed.