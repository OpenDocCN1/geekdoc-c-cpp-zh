
# Quiz

1. Can a particular array contain integers, floats, and characters?
2. What is the number of the starting index of an array?
3. What is the number of the ending index of an array?
4. What is the difference between initialization and assignment?
5. What are the two alternative methods of initializing an array?
6. What is the purpose of the null character?
7. What is the value of the name of an array?
8. Should the last element of a character array always be a null character?
9. What is the difference between the get and getline functions of the cin object?
10. When you pass an array name as a function argument, are you passing it by value, reference, or address?

# Chapter 11: What’s the Address? Pointers

## Overview

My parents told me when I was a child that it was not to point. However, each semester I teach my computer students how to point. No, I am not trying to promote rude behavior. Rather, I am teaching my students about pointers, which "point" to another variable or constant.

You yourself may have acted as a pointer in the past. Have you ever been asked where someone lives? If that house was nearby, you may have pointed it out.

The pointer performs a similar function. A pointer points to another variable or constant. Of course, the pointer does not point with an arm and fingers as you would. Rather, the pointer’s value is the address of the variable or constant to which it points. Indeed, you may have done something similar. If you were asked where someone lives and that house was not close enough to physically point out, you instead may have provided an address by which the house could be located.

Pointers have had a reputation among programming students for being difficult to learn. I think they are not difficult if you take the time to understand what they do. In any event, difficult or not, it is important to learn about pointers. Some C++ tasks are performed more easily with pointers, and other C++ tasks, such as dynamic memory allocation, cannot be performed without them.

So, on that note, let’s learn how to create and work with pointers.

# Declaring a Pointer

Like any variable or constant, you must declare a pointer before you can work with it. The syntax of declaring a pointer is almost the same as declaring a variable that stores a value rather than an address. However, the meaning of the pointer's data type is quite different than the meaning of the data type of a variable that stores a value rather than an address.

# Syntax of a Pointer Declaration

The syntax of declaring a pointer is almost the same as the syntax of declaring the variables we have worked with in previous chapters. The following statement declares an integer variable:

```
int* iPtr;
```

The asterisk you use to declare a pointer is the same asterisk that you use for multiplication. However, in this statement the asterisk is being used in a declaration, so in this context it is being used to designate a variable as a pointer. Later in this chapter, we will use the asterisk for a third, as an indirection operator.

**Note**: It is common in C++ for a symbol to have different meanings depending on the context. For example, an ampersand (&) in an argument list means you are passing an argument by reference, whereas an ampersand in front of a variable is the address-of operator.

The integer variable can also be declared with the asterisk preceding the variable name instead of following the data type:

```
int *ptr;
```

Either alternative is equally correct because the compiler generally ignores spaces between an operator and a variable name, constant name, or number. Indeed, the following pointer declaration works also:

```
int *ptr;
```

My preference is the first example, in which the asterisk follows the data type and is separated by a variable name, since (in my opinion) it signifies that the variable is a pointer. However, all three syntaxes are correct. In of these variations, the only difference between declaring a pointer variable and a variable that stores a value rather than an address is the asterisk between the data type and the pointer name.

# The Meaning of Pointer Data Types

While the syntax of declaring a pointer is almost the same as declaring the variables and constants which store a value rather than an address, the meaning of the data type in the declaration of a pointer is different than the declaration of other variables and constants.

With the examples we have worked with previously, the data type in the variable declaration describes what data can be stored in that variable. Thus, the value of an integer variable or constant is an integer, the value of a character variable or constant is a character, and so.

However, with a pointer, the data type in the declaration means something different, namely the data type of another variable (or constant) whose memory address is the value of the pointer. In other words, the value of an integer pointer must be the address of an integer variable or constant, the value of a float pointer must be the address of a float variable or constant, and so forth.

The actual type of the value of all pointers, whether integer, float, character, or otherwise, is the same, a hexadecimal number that represents a memory address. The only difference between pointers of data types is the data type of the variable or constant that the pointer points to. This is demonstrated by the following program, which uses the sizeof operator to show that the sizes of pointers of different data types are the same (a long data type uses 4 bytes by operating system and compiler) even though the different data types (int, float, char) are not all the same size:

```cpp
#include <iostream>
using namespace std;

int main() {
    int* iPtr;
    float* fPtr;
    char *cPtr;
    cout << "The size of iPtr is " << sizeof(iPtr) << endl;
    cout << "The size of fPtr is " << sizeof(fPtr) << endl;
    cout << "The size of cPtr is " << sizeof(cPtr) << endl;
    return 0;
}
```

The output is therefore:

The size of iPtr is 4
The size of fPtr is 4
The size of cPtr is 4

Otherwise, a pointer is similar to the variables or constants we have studied previously. A pointer itself may be a variable or a constant, and like other variables or constants, it is also stored at a memory address. What distinguishes a pointer is that its value is the memory address of another variable or constant.

![](img/59a3417a6d5906fae6d8000d4c2cff76_203_0.png)

# Assigning a Value to a Pointer

This section will explain how you assign a value to a pointer. Though, before I explain how, perhaps I explain why.

# Why You Should Not Try to Use an Unassigned Pointer

Back in elementary school we were taught a verse: "I shot an arrow into the air, where it lands, I don't." Looking back, I wonder when young children were taught this verse. Maybe rhyme, but its message is not appropriate for little ones. However, when you declare a pointer then use it without first assigning it a value, you are, alas, doing the programming equivalent of that.

The following program declares a pointer and attempts to output its value without first assigning it a value:

```cpp
#include <iostream>
using namespace std;

int main()
{
    int* iPtr;
    cout << "The value of iPtr is " << iPtr << endl;
    return 0;
}
```

The runtime, depending on your compiler and operating system, may be a compiler error, a runtime error, or a crash. Regardless, attempting to use a declared pointer without first assigning it value is not a good idea.

As you may recall from previous chapters, when you declare a variable and attempt to output its value without first assigning it, the result is a so-called "garbage value" that makes little sense. The reason for this is the computer attempts to interpret whatever value is left over from previous programs at the address of the variable.

When the variable is a pointer, leftover value is interpreted as another memory address, which the pointer tries to access when you attempt to use it. There are a number of memory address ranges that you are not permitted to access programmatically, such as those reserved for the operating system. If the leftover value is interpreted as one of those prohibited addresses, the result is an error.

# Null Pointers

If it is too early in your code to know which address to assign to the pointer, then you first assign the pointer NULL, which is a constant with a value of zero defined in several standard libraries, including *iostream*. The following program does:

```cpp
#include <iostream>
using namespace std;

int main()
{
    int* iPtr;
    iPtr = NULL;
}
```
