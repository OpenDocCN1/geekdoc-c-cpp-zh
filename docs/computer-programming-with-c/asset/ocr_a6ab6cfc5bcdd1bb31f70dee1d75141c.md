# 9.3.1  Program to arrange n-books in ascending order of price: An example

Let us create a program to accept details of n different books as input from the user and to arrange the books in ascending order of their price. We will store the details of n-books entered by the user in an array of type Book. Therefore, the size of the array that we need to create must at least be n. Recall from Chapter 6, Section 6.2.2, we will not be able to actually specify the size of the array in terms of n because the value of variable n will be known at run time, whereas the compiler needs to allocate the memory for an array at the compile time. Hence, we create this program by assuming the maximum limit of value of n as 100. We create an array with a capacity 100 by using the following statement:

```
```cpp
struct Book b[100];
```
```

This means that the array b can store at the most 100 objects inside it, and the elements of the array will therefore be indexed from 0 to 99 as shown in the Figure 9.16. Note that, all the elements of the array will have junk values unless we initialize the values explicitly.

![](bbox=[0.125, 0.401, 0.851, 0.672])

Although we have created a space large enough to accommodate 100 Book objects, it does not mean that a user should always store the details of 100 books in the memory. This is because, the user might actually require storing the details for different number of books each time the program is executed. Hence, before we start taking the actual array elements as input from the user, we will ask the user about the number of Book objects that the user wishes to store, to arrange the objects in ascending order of price. As seen in the code, we create a variable n as an integer variable, that will store the ‘number of objects’ that user will input, to store them in an array. Therefore, the first step of the program will now be to take the value of n as input as shown below:

```
```cpp
int n;
printf("How many Books?\n");
scanf("%d",&n);
```
```