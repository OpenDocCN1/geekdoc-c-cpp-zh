# Chapter 12 673

Addresses and Pointers

Another way of looking at references is to consider them as pointers with restricted capabilities that hide a lot of the dereferencing with pointers. For example, take look at these statements:

```
int b; // b is an integer variable
int&a = b; // a is a reference variable that stores b's address
a = 10; // this changes b's value to 10
```

Here, a is declared as a reference variable that effectively changes a named constant for the address of b. Because the compiler knows from the declaration that a is a reference variable, it automatically assigns b's address (rather than b's contents) to a in the declaration statement. Finally, in the statement a = 10;, the compiler uses the value stored in a to change the value stored in b to 10. The advantage of using the reference is that it accesses b's value without having to use the induction operator, *. As noted previously, this type of access is referred to as an automatic dereference.

The following sequence of instructions makes use of this same correctness between a and b using pointers:

```
int b; // b is an integer variable
int *a = b; // a is a pointer - store b's address in a
a = 10; // this changes b's value to 10 by explicit
// dereference of the address in a
```

Here, a is defined as a pointer to store the address of b. Therefore, *a (which can be read as "the variable address is a" or "the variable pointed to by b") is b, and the expression *a = 10 changes b's value to 10. Notice that with pointers, the stored address can be altered to point to any other variable except the one it's initialized to. Also, notice that a reference variable cannot be altered except with references; to dereference a, you must use the indirection operator, *. As you might expect, the * is also called the dereferencing operator.

![](bbox=[0.109, 0.597, 0.168, 0.633])

# EXERCISES 12.1

+   1. (For) If average is a variable, what does &average mean?
2. (Practice) For the variables and addresses shown in Figure 12.7, determine the addresses corresponding to the expressions &temp, &dist, &date, and &miles.
3. (Practice) Write a C++ program that includes the following declaration statements. Have the program use the address operator and a cout statement to display the addresses corresponding to each variable.

```
int num, count;
long date;
float slope;
double power;
```

+   b. After running the program for Exercise 3a, draw a diagram of how your computer has set aside storage for the variables in the program. On your diagram, fill in the addresses the program displays.