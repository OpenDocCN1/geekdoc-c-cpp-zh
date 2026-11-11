4. Define the concept of 2-D Array. Write a program to input two 3×3 matrices and print the multiplication of both the matrices

or

Define the concept of pointer. Also define the dynamic memory allocation and various functions for dynamic memory allocation.

5. Define the concept of sorting and write a program to input 10 named and then sort that name in ascending order.

or

Differentiate between function and macros and write a program to input two numbers and print the max. Number with the help of macro.

# Model Question Paper 2
[MODEL QUESTION PAPER] ECS-101
B.Tech.
FIRST/SECOND SEMESTER EXAMINATION
COMPUTER CONCEPTS AND PROGRAMMING IN ‘C’

M.M. 200

Time: 3 Hrs

# SECTION A

1. Attempt all 20 questions. (20×1=20)

+   (a) Which of the following is evaluated first?
+      i. &&
+      ii. ||
+      iii. !

+   (b) Which is not valid in C?
+      i. class a Class{public:int x;};
+      ii. /* A comment */
+      iii. char x=12;

+   (c) Which of the following is not a valid declaration for main()?
+      i. int main()
+      ii. int main(int argc, char *argv[])
+      iii. They both work

+   (d) Evaluate as true or false: !(1 && 0 || 1 !1)
+      i. True
+      ii. False
+      iii. Invalid statement

+   (e) What operator is used to access a struct through a pointer?
+      i. ->
+      ii. >>
+      iii. *

+   (f) Which uses less memory?
+      i. struct astruct
+      {
+         int x;
+         float y;
+         int v;
+      };
+      ii. union aunion
+      {
+         int x;
+         float v;
+      };
+      iii. char array[10];

+   (g) What do non global variables default to:
+      i. static
+      ii. auto
+      iii. register

+   (h) Evaluate !(1&&1||1&&0)
+      i. Error
+      ii. True
+      iii. False

(i) Code:

```
int z,x=5,y=10,a=4,b=2;
z = x++ - y * b / a;
```

What number will z in the sample code above contain?
   i. 5
   ii. 6
   iii. 10
   iv. 11
   v. 12

+   (j) What function will read a specified number of elements from a file?
+      i. fileread()
+      ii. getline()
+      iii. readfile()
+      iv. fread()
+      v. gets()

+   (k) int testarray[3][2][2] = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12};
+   What value does testarray[2][1][0] in the sample code above contain?
+      i. 3
+      ii. 5
+      iii. 7
+      iv. 9
+      v. 11

(l) Code:

```
int a=10,b;
b=a+++ ++a;
printf("%d, %d, %d, %d",b,a++,a++);
```