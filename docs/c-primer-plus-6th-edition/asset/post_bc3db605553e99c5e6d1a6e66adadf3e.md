
## Chapter 4 Compound Types

## Pointers and Numbers

Pointers are not integer types, even though computers typically handle addresses as integers. Conceptually, pointers are distinct types from integers. Integers are numbers you can add, subtract, divide, and so on. A pointer describes a location, and it doesn't make sense, for example, to multiply two locations by each other. In terms of the operations you can perform with them, pointers and integers are different from each other. Consequently, you can't simply assign an integer to a pointer:

```cpp
int *pt;
pt = 0xB8000000; // type mismatch
```

Here, the left is a pointer to it, so you can assign it to an address, but the right side is just an integer. You might know that 0xB8000000 is the combined segment-offset address of video memory on your computer system, but nothing in the statement tells the program this is an address. C prior to C99 lets you make assignments like this. C++ more stringently enforces type agreement, and the compiler will give you an error message saying you have a mismatch. If you want to use a numeric value as an address, you should use a type cast to convert the number to the appropriate address type:

```cpp
int *pt;
pt = (int *)0xB8000000; // types now match
```

Now both sides of the assignment represent addresses of integers, so the assignment is valid. Note that just because it is an address of a type `int` value it doesn't mean that `pt` itself is an int. For example, one might have a platform for which type `int` is a 2-byte value and the addresses are 4-byte values.

Pointers have some other interesting properties that we'll discuss as they become relevant. Meanwhile, let's look at how pointers can be used to manage runtime allocation of memory space.

## Allocating Memory with new

Now that you have a feel for how pointers work, let's see how they can implement the important technique of allocating memory as a program runs. So far, you've initialized pointers to the addresses of variables; the variables are `named` memory allocated during compile time, and each pointer provides an alias for memory you could access directly by name. The true worth of pointers comes into play when you allocate `unnamed` memory during runtime. In this case, pointers are the only access to memory. In C, you can allocate memory with the library function `malloc()`. You can still do so in C++, but C++ also has the `new` operator.

Let's try this new technique by creating unnamed runtime storage for a type int and accessing the value with a pointer. The key is the C++ new operator. You tell new for what data type you want memory; new finds a block of the correct size and

## Pointers and the Free Store

returns the address of the block. You assign this address to a pointer, and you're in business.
Here's an example of the technique:

```cpp
int * pn = new int;
```

The `new int` operator tells the program you want some new storage for holding an int. The new operator uses the type to figure out how many bytes are needed. Then it finds the memory and returns the address. Next, you assign the address to pn, which is declared to be a pointer to int. Compare this with assigning the address of a variable to a pointer:

```cpp
int higgens;
int * pt = &higgins;
```

In both cases (pn and pt), you assign the address of an int to a pointer. In the second case, you can also access the int by name: higgens. In the first case, your only access is via the pointer. That raises a question: Because the memory which pn points lacks a name, what do you call it? We say that pn points to a data object. This is not "object" in the sense of "object-oriented programming"; in the sense of "thing." The term "data object" is more general than the term "variable" because it means any block of memory allocated for a data item. Thus, a variable is also a data object, but the memory to which pn points is not. The pointer method for handling data objects may seem awkward at first, but it offers greater control over how your program manages memory.

The general form for obtaining and assigning memory for a single data object, which be be a structure as well as a fundamental type, this is:

```cpp
typeName * pointer_name = new typeName;
```

You use the data type twice: once to specify the kind of memory requested and once to declare a suitable pointer. If you've already declared a pointer of the correct type, you can use it rather than declare a new one. Listing 4.17 illustrates using new with different types.

## Listing 4.17 use_new.cpp

```cpp
// use_new.cpp -- using the new operator
#include <iostream>

int main() {
    using namespace std;
    int nights = 1001;
    int * pt = new int; // allocate space for an int
    *pt = 101; // store a value there

    cout << "nights value = " << nights << ": location = " << &nights << endl;
    cout << "int = " << &pt << endl;
    cout << "value = " << *pt << ": location = " << pt << endl;

double *pd = new double; // allocate space for a double
*pd = 1000001.0; // store a double there

cout << "double = " << &pd << endl;
cout << "value = " << *pd << ": location = " << pd << endl;

delete pt;
delete pd;

return 0;
}
```
