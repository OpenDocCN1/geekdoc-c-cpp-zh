
Here the first argument signifies the number of names to be entered, whereas the second argument[length] signifies the maximum length that a name can take.

Program that input 10 names has been discussed here.

Program: Write a program that can accept 10 names, also display the output

## Solution

```
char name[10][40];
void main
{
int i=0, j=0;
cout<<"enter 10 names";
for(i=0;i<=9;i++)
cin>>name[i];
cout<<" here is the output of names";
for(i=0;i<=9;i++)
cout<<name[i]<<endl;
}
```

It is significant that the reader should learn, that the elements of two dimensional character array can be easily accessed with the help of pointers.

## 2.4 POINTERS

Pointer is a variable that is capable to hold the address of another variable. Holding of addresses of another variable is needed in various instances that include:

- To access the array element
- To change the value of variable from function
- In dynamic allocation of memory.
- In complex programming, such as link list, tree, B tree etc.

To denote that a specific variable is acting as a pointer, they are preceded with the symbol '*'. For instance, int *x, Here the pointer is integer type. It means that this pointer can hold the address of integer type variable.

### 2.4.1 Declaring pointers

As already stated that pointer is a variable that is capable to hold the address of another variable, correspondingly, we need a variable whose address can be stored in the pointer and consequently, we can access the variable with the help of pointer. To declare the pointer, variable name is preceded with asterisk (*) symbol, same has been illustrated in the following program.

```
int x=8;
int *p;// variable that is pointer of int type
p=&x; //p now holds the address of variable x
cout<<p;   // print the address of x;
cout<<*p;   // print the value pointed by p;
```

Working of the above statements has been illustrated in the figure 2.5. Initially, the variable 'x' is declared and assumes that it has been allocated the address location 1000. Similarly, when int *p is declared, it is also allocated the address similar to any other variable. Here we have assumed that the pointer 'p' is allocated new address which is at memory location of 1010. Consequently, we can conclude that both are different variables and definitions applicable to variable is still applicable on pointer variables. In addition, operations applicable to pointer variable can also be applied on them.

### 2.4.2 Accessing the pointer variables

Pointer is also a variable but instead of holding the value it holds the address of another variable. We are assuming that it is holding the address of variable 'x' that is having the address 1000. Now, it will have the address of 1000 in its value part, as illustrated in the figure 2-5. Once user is displaying the value of this pointer, he will get this address as value.

![](img/9b7c80a1312a664ae505ba138aa3306b_49_0.png)

However, it facilitates to access the variable whose address is held by the pointer. To access the value stored in the address held by the pointer we use de-referencing operator. To denote the de-referencing, the statement *p is used. Consequently, it displays the value stored at that address. Usage of pointer has been depicted in the following program.

```
// Program to display the use of pointer
int x=8;
int *p;
p=&x;
cout<<" value of x "<<x // 8
cout<<" value of p="<<p //1000
cout<<" value pointed by *p"<<*p;   // 8 will be printed
```

## Data Structure Simplified

```
```cpp
*p=30;

cout<<" value of x"<<x; // 30

cout<<" value of p="<<p;          1000

cout<<" value of *p="<<*p;    // 30
```
```

Pointers are widely used in the character array (string). Similarly, pointers are also used in integer array. Pointer usage in array has been depicted in the subsequent sections.

### 2.4.3 Pointer to pointer

Sometimes, we need to store the address of a pointer, this can be accomplished with the help of pointer to pointer. Pointer to pointer is a variable that holds the address of another variable that is pointer type.

#### Declaring pointer to pointer

Declaring pointer to pointer is different from the normal pointer type. In pointer to pointer notation two asterisk (**) are preceded before the identifier.

- int **pp;             (2.4.1)
- int *p;                (2.4.2)
- pp=&p;                 (2.4.3)

In the line 2.4.1, a variable declared is pointer to pointer type. It is capable of storing the address of another pointer variable. Notation to store the address of pointer in the ‘pointer to pointer’ has been depicted in the line 2.4.3. Usage of pointer to pointer type has been depicted with the help of following example.

```
```cpp
// Program to display the use of double pointer
#include<iostream.h>
#include<conio.h>
int main()
{
int v=20;
int *p;
int **pp;
// Assigning address to pointer
p=&v;
pp=&p;
cout<<"value of v="<<v<<endl;
cout<<"Address of v="<<&v<<endl;
cout<<"Address held by p="<<p<<endl;
cout<<" Address of p="<<&p<<endl;
```

```
cout<<"Valued de-referenced of p:"<<*p<<endl;
cout<<" Address of pp:"<<&pp<<endl;
cout<<"Address hold by pp:"<<pp<<endl;
cout<<"Valued de-referenced of *pp:"<<*pp<<endl;
cout<<"Valued de-referenced of **pp:"<<**pp<<endl;
getch();
return 0;
}
```

## Output

Value of v=20;

Address of v=0xfc1fff4

Address of *p=0xfc1fff2 // Now address of p

Address held by p=0xfc1fff4   //Address hold by p (i.e. of v)

Valued de-referenced of p=20  //de-referencing the value of p (i.e. of v)

Address of pp=0xfc1fff0      // Now address of pp

Address held by pp=0xfc1fff4  //Address hold by pp (i.e. of p)

Valued de-referenced of pp=20 // de-referencing the value of pp(i.e. of v)

### 2.4.4 Use of Pointers in an Array

Pointers are widely used in arrays. To access the array element, we can initialized the index of an array to a pointer variable. For instance, in the array ‘a’, we have initialized it with list of numbers. Accessing of array element with the help of pointer has been depicted in the following program.

```
// Program to access the array element with the help of pointers
int main()
{
int a[]={10,50,20,40,70};
int *x;
x=&a[0];
cout<<x<<endl;
cout<<*x;        //output 10
cout<<*(x+2);        // output 20
cout<<a[2];     // output 20
cout<<*(x+3);        // output 40
```

```
```cpp
cout<<a[3];        // output 40

return 0;
}
```
```

In the above program, pointer is initialized with the base address of an array. Consequently, statement *x displays the element stored at the index ‘0’. When the statement *(x+2) is used, it signifies that the 2 is to be added at the base address which results in x[2]. Consequently, the element accessed by the *(x+2) and x[2] gives the same result. In the same line, the statement *(x+3) will result in 0+3 i.e. 3rd index. Correspondingly, the element stored at the 3rd index will be accessed.

### 2.4.5 Dynamic Array creation

During the array creation, array size can be allocated either at runtime or at compile time. Accordingly, it can be classified as:

- Static array
- Dynamic array

Array whose size is allocated at compile time, such arrays are known as static array. Arrays that have been discussed in the previous sections fall under the category of static array.

Other type of array is dynamic array, space to dynamic array is allocated at run time. In C++, creation of dynamic array is accomplished with the help of new operator. Same has been depicted with help of following example.

```
```cpp
Program: Create the dynamic array and discuss their various ways of initialization.

Solution:

#include<iostream.h>

#include<conio.h>

int main()
{
int *x;

int *y;
y=new int(45);
x=new int[4];
clrscr();
// elements initialization will follow
x[0]=90;
x[1]=55;
x[2]=32;
```

```
```cpp
x[3]=67;

// From this statement onwards dynamic array will be created.
int i=0;
cout<<"Dynamic array elements are"<<endl;
while(i<3)
{
cout<<"x[i] i="<<i<<"  "<<x[i]<<endl;
i++;
}
cout<<"y ="<<*y<<endl;
getch();
return 0;
}
```
```

```
```cpp
// Program to initialize the dynamic pointer.
#include<conio.h>
int main()
{
int *y;
clrscr();
y=new int(45);
int i=0;
cout<<"y ="<<*y<<endl; //Output will be 45
getch();
return 0;
}
```
```

### 2.4.6 Array of pointers

Array of pointers is an array that holds the pointers (addresses). Usage of array pointer is significant in cases where we need to store the addresses of various pointers of similar type. Array of pointer facilitate the ease of accessibility at the same time improves the efficiency of the program written. Primarily array of pointer is used to deal with double dimensional array type of problems. For instance, if we intend to store two or more arrays, then we can use pointer arrays. Example to access three array using array of pointers has been depicted in the following program.
