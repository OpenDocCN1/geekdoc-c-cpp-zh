
Assuming that the value of the pointer variable p has not changed (so it still points to the same dynamic variable), how can you destroy this new dynamic variable and return the memory it uses to the freestore manager so that the memory can be reused to create other new dynamic variables?

7. Write a definition for a type called NumberPtr that will be the type for pointer variables that hold pointers to dynamic variables of type double. Also, write a declaration for a pointer variable called myPoint, which is of type NumberPtr.

8. Describe the action of the new operator. What does the new operator return? What are the indications of errors?

## TYPE DEFINITIONS

You can assign a name to a type definition and then use the type name to declare variables. This is done with the keyword typedef. These type definitions are normally placed outside the body of the main part of your program and outside the body of other functions, typically near the start of a file. That way the typedef is global and available to your entire program. We will use type definitions to define names for pointer types, as shown in the example below.

## SYNTAX

```
typedef Known_Type_Definition New_Type_Name;
```

## EXAMPLE

```
typedef int* IntPtr;
```

The type name IntPtr can then be used to declare pointers to dynamic variables of type int, as in the following example:

```
IntPtr pointer1, pointer2;
```

## POINTERS AS CALL-BY-VALUE PARAMETERS

When a call-by-value parameter is of a pointer type, its behavior can occasionally be subtle and troublesome. Consider the function call shown in Display 10.4. The parameter temp in the function sneaky is a call-by-value parameter, and hence it is a local variable. When the function is called, the value of temp is set to the value of the argument p and the function body is executed. Since temp is a local variable, no changes to temp should go outside the function sneaky. In particular, the value of the pointer variable p should not be changed. Yet the sample dialogue makes it look like the value of the pointer variable p has changed. Before the call to the function sneaky, the value of *p was 77, and after the call to sneaky the value of *p is 99. What has happened?

The situation is diagrammed in Display 10.5. Although the sample dialogue may make it look as if `p` were changed, the value of `p` was not changed by the function call to `sneaky`. Pointer `p` has two things associated with it: `p`'s pointer value and the value stored where `p` points. But the value of `p` is the pointer (that is, a memory address). After the call to `sneaky`, the variable `p` contains the same pointer value (that is, the same memory address). The call to `sneaky` has changed the value of the variable pointed to by `p`, but it has not changed the value of `p` itself.

If the parameter type is a class or structure type that has member variables of a pointer type, the same kind of surprising changes can occur with call-by-value arguments of the class type. However, for class types, you can avoid (and control) these surprise changes by defining a copy constructor, as described later in this chapter.

### Display 10.4  A Call-by-Value Pointer Parameter (part 1 of 2)

```
//Program to demonstrate the way call-by-value parameters
//behave with pointer arguments.
#include <iostream>
using std::cout;
using std::cin;
using std::endl;

typedef int* IntPointer;

void sneaky(IntPointer temp);

int main()
{
    IntPointer p;

    p = new int;
    *p = 77;
    cout << "Before call to function *p == "
         << *p << endl;

    sneaky(p);

    cout << "After call to function *p == "
         << *p << endl;

    return 0;
}
```

### Display 10.4 A Call-by-Value Pointer Parameter (part 2 of 2)

```
21 void sneaky(IntPointer temp)
22 {
23   *temp = 99;
24   cout << "Inside function call *temp == "
25       << *temp << endl;
26 }
```

## SAMPLE DIALOGUE

> Before call to function *p == 77
> Inside function call *temp == 99
> After call to function *p == 99

### Display 10.5 The Function Call sneaky(p);

+   1. Before call to sneaky:

![](img/9505fd46e120aa9c1406715936ff6251_415_0.png)

+   2. Value of p is plugged in for temp:

![](img/9505fd46e120aa9c1406715936ff6251_415_1.png)

+   3. Change made to *temp:

![](img/9505fd46e120aa9c1406715936ff6251_415_2.png)

+   4. After call to sneaky:

![](img/9505fd46e120aa9c1406715936ff6251_415_3.png)

## USES FOR POINTERS

Chapter 17 discusses ways to use pointers to create a number of useful data structures. This chapter only discusses one use of pointers, namely, to reference arrays, and in particular to create and reference a kind of array known as a dynamically allocated array. Dynamically allocated arrays are the topic of Section 10.2.

## 10.2 Dynamic Arrays

In this section you will see that array variables are actually pointer variables. You will also find out how to write programs with dynamically allocated arrays. A **dynamically allocated array** (also called simply a **dynamic array**) is an array whose size is not specified when you write the program, but is determined while the program is running.

### ARRAY VARIABLES AND POINTER VARIABLES

Chapter 5 described how arrays are kept in memory. At that point we discussed arrays in terms of memory addresses. But a memory address is a pointer. So, in C++ an array variable is actually a kind of pointer variable that points to the first indexed variable of the array. Given the following two variable declarations, p and a are both pointer variables.

```
int a[10];
typedef int* IntPtr;
IntPtr p;
```

The fact that a and p are both pointer variables is illustrated in Display 10.6. Since a is a pointer that points to a variable of type int (namely, the variable a[0]), the value of a can be assigned to the pointer variable p as follows:

```
p = a;
```

After this assignment, p points to the same memory location that a points to. Thus, p[0], p[1], . . . p[9] refer to the indexed variables a[0], a[1], . . . a[9]. The square bracket notation you have been using for array variables to point to pointer variables as long as the pointer variable points to an array in memory. After the above assignment, you can treat the identifier p as if it were an array identifier. You can also treat the identifier a as if it were a pointer variable, but there is one important reservation: *You cannot change the pointer value in an array variable.* If the pointer variable p2 has a value, you might be tempted to think the following is legal, but it is not:

```
a = p2; //ILLEGAL. You cannot assign a different address to a.
```

The underlying reason why this assignment does not work is that an array variable is not of type int*, but its type is a constant version of int*. An array variable, like a, is a pointer variable with the modifier const, which means that its value cannot be changed.

(An array variable is actually more than an ordinary pointer variable since it carries some additional size information about the array, but an array variable does include a pointer to the array and the array variable can be assigned to a pointer variable. So, an array variable is a kind of pointer variable and can be treated like a pointer variable whose value cannot be changed.)

### Display 10.6 Arrays and Pointer Variables

```
//Program to demonstrate that an array variable is a kind of pointer variable.
#include <iostream>
using std::cout;
using std::endl;

typedef int* IntPtr;

int main()
{
    IntPtr p;
    int a[10];
    int index;

    for (index = 0; index < 10; index++)
        a[index] = index;

    p = a;

    for (index = 0; index < 10; index++)
        cout << p[index] << " ";
    cout << endl;

    for (index = 0; index < 10; index++)
        p[index] = p[index] + 1;

    for (index = 0; index < 10; index++)
        cout << a[index] << " ";
    cout << endl;

    return 0;
}
```

> Note that changes to the array p are also changes to the array a.

## SAMPLE DIALOGUE

```
0 1 2 3 4 5 6 7 8 9
1 2 3 4 5 6 7 8 9 10
```

## CREATING AND USING DYNAMIC ARRAYS

One problem with the kinds of arrays we discussed in Chapter 5 is that you must specify the size of the array when you write the program—but you may not know what size array you need until the program is run. For example, an array might hold a list of student identification numbers, but the size of the class may be different each time the
