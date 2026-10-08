
int *large(int *, int *);
/* main 函数开始 */
main()
{
/* 声明变量 */
int i_first, i_second, *i_large;

/* 接受值 */
printf("\n Enter the values of number 1 and number 2 : ");
scanf("%d %d", &i_first, &i_second);

/* 调用函数 large */
i_large = large(&i_first, &i_second);
/* 显示两个数中较大的一个 */
printf("\n the larger number is %d\n", *i_large);
return;
}
/* main 函数结束 */

/* 返回指向整数的指针的函数 */
/* large 函数开始 */
int *large(int *i_first, int *i_second)
{
if (*i_first > *i_second)
return i_first;
else
return i_second;
}

/* large 函数结束 */

# 输出：

Enter the values of number 1 and number 2 : 40 10
The larger number is 40

程序 14 包含一个名为 large 的函数，该函数接受两个参数。由调用函数传递的两个参数都是地址，因此使用指针来接收这些地址。large 函数确定这两个数中较大的一个，并返回包含较大值的变量的地址。因此，在调用函数中，使用指针变量 i_large 来接收返回的地址。请注意，在函数 large 的原型中，我们使用了语句 int *large(int *, int *)。此处函数名 large 前的 * 表示该函数返回的值是指向整数的指针。注意，函数可以返回在调用函数中定义的变量的地址。如果函数返回在函数内部局部定义的变量的地址，则会发生错误。

## 函数指针

我们知道，指针可以指向任何标准 C 数据类型，例如整数、浮点数或字符。当数组名用于表达式中时，它给出数组第一个元素的地址。类似地，函数名代表其起始地址。因此，我们也可以定义一个指向函数的指针。一旦定义，这样的指针就可以用于调用函数。声明函数指针的语法如下：

```
data type (*func_pointer)( data type of function parameters);
```

其中 func_pointer 是一个变量名，可以存储函数的地址。星号 (*) 运算符位于函数指针变量之前。函数指针的声明还包括函数将接受的参数的数据类型以及函数将返回的值的类型。要声明一个指向程序 13 中编写的函数 exchange 的函数指针，使用以下语法：

```
void (*funp_exchange) (int *, int *);
```

其中 *funp_exchange 是一个指针变量，存储接受两个指针变量作为参数且不返回任何值的函数的地址。

注意，术语 *funp_exchange 写在括号内。这里的括号很重要，因为它区分了函数指针和返回指针值的函数。如果前面的定义修改为 void *funp_exchange (int *, int *);，则该定义指的是名为 funp_exchange 的函数，它接受两个指针变量并返回一个 void 指针。因此，用户在使用函数指针时需要谨慎。程序 15 说明了函数指针的使用：

## 程序 15

```c
/*Program to illustrate pointer to function*/
#include<stdio.h>

/* Function prototype declaration*/
int add(int, int);

/*Beginning of function main */
main( )
{
   /* Declare variables */
   int i_first, i_second, i_ans;
   int (*funp_add)(int, int);    /* Function Pointer */
   /*Assigning address of a function add to a function pointer*/
   funp_add = add;

   /* Accept data */
   printf("\nEnter first number: ");
   scanf("%d",&i_first);

   printf("\nEnter second number: ");
   scanf("%d",&i_second);

   /* Call a function */
   i_ans = (*funp_add)(i_first, i_second);
   /* Print output */
   printf("\nThe sum of two integers %d and %d is %d\n", i_first, i_second, i_ans);
}
/* End of function main */

/* Beginning of function add */
int add(int i_first, int i_second)
{
	return(i_first + i_second);
}
/* End of function add */
```

**输出：**

```
Enter first number: 6
Enter second number: 7
The sum of two integers 6 and 7 is 13
```

程序 15 中的函数 add 接受两个参数；然后对接受的值执行加法运算，并返回结果。在 main 函数中，语句 int (*funp_add) (int, int) 声明了一个名为 funp_add 的函数指针，它可以存储函数的地址，该函数可以接受两个整数参数并返回一个整数值。

在程序 15 的执行过程中，使用语句 funp_add=add 将函数 add 的地址赋值给变量 funp_add。然后通过语句 i_ans = (*funp_add)(i_first, i_second) 调用函数 add。函数返回的结果被赋值给变量 i_ans，并通过 printf() 函数在屏幕上显示。

## 12.7 指针与结构

我们讨论过，数组名充当指向数组的指针。结构体也是类似的情况。结构体名可以充当指向整个结构体的指针。因此，可以使用结构体名访问结构体的每个成员。然而，访问数组成员的方式与访问结构体成员的方式有很大不同。原因是结构体成员具有不同的数据类型，因此每个成员占用的存储空间不同。因此，用于数组的指针算术计算在结构体中不起作用。结构体指针的声明与其他指针变量类似。例如，要定义 ptrcontact 为结构体指针，ptrcontact 前必须加上 * 符号：

```
struct contact
{
char c_name[30];

unsigned long int li_phoneno;
char c_email[50];
} *ptrcontact, contact1;

ptrcontact= contact1;
```

普通结构体和指针结构体在使用上的区别在于访问变量的方式。如第 11 章所述，使用点 (.) 运算符来访问结构体的各个成员。然而，要使用结构体指针访问结构体成员，则使用箭头 (->) 运算符。例如，要扫描 c_name 的值，将使用 scanf("%[^
]", ptrcontact->c_name)。让我们编写一个程序来理解结构体指针是如何工作的。程序 16 说明了结构体指针的使用。

## 程序 16

```c
/* Program to illustrate pointer to a structure*/
#include<stdio.h>
/* Beginning of function main */
main()
{
/* Declare variables */
struct contact
{
char c_name[25];
char c_email[30];
unsigned long int li_phoneno;
};contact1,*ptrcontact;
char c_temp;
ptrcontact=&contact1;
/* Accept values of structure members from user*/
printf("\n Enter name : ");
scanf("%[^\n]",ptrcontact->c_name);
c_temp=getchar();
printf("\n Enter e-mail address : ");
scanf("%[^\n]",ptrcontact->c_email);
printf("\n Enter phone number : ");
scanf("%ld",&ptrcontact->li_phoneno);

/* Display values of structure members of contact*/
printf("\nThe values recently entered by you are as under:\n ");
printf(" Name : %s",ptrcontact->c_name);
printf("\n E-mail address : %s",ptrcontact->c_email);
printf("\n Phone number : %d\n", ptrcontact->li_phoneno);
return;
}
/* End of function main */
```

**输出：**

Enter name : Harshit Jain

Enter e-mail address: harshjain@gmail.com

Enter phone number: 5412363

The values recently entered by you are as under
Name : Harshit Jain
E-mail address: harshjain@gmail.com
Phone number: 5412363

在程序 16 中，赋值语句 ptrcontact=&contact1; 将结构体 contact1 的第零个元素的地址赋值给 ptrcontact。结构体 contact1 的成员通过指针变量 ptrcontact 访问。使用箭头运算符 (->) 来访问成员。注意，也可以使用另一种方式 (*ptrcontact).c_name 来访问结构体的成员。

结构体指针可用于在函数内部操作结构体的值。我们在第 11 章中讨论了将结构体作为函数参数传递。然而，如果在函数中修改了结构体成员的值，这种变化不会反映在调用函数中。如果将结构体指针作为参数传递，修改将直接作用于内存位置，因此会反映在调用函数中。让我们编写一个程序，查看结构体指针的使用。

程序 17 说明了将结构体指针作为函数参数传递的用法。

## 程序 17

```c
/* Program to illustrate pointer to a structure passed as a function
parameter */
#include<stdio.h>
/* Definition of structure */
struct contact
{
char c_name[25];
char c_email[30];
unsigned long int li_phoneno;
};
/* Function prototype */
void getcontact(struct contact *);
/* Beginning of function main */
main()
{
/* Declaring structure variable */
struct contact contact1, *ptrcontact;
char c_temp;
/*Assigning address of a structure contact to pointer variable */
ptrcontact=&contact1;
/* Function call to getcontact */
getcontact(ptrcontact);
/* Print the value of structure */
printf("\nThe values recently entered by you are as under : \n ");
printf(" Name : %s",ptrcontact->c_name);
printf("\n E-mail address : %s",ptrcontact->c_email);
printf("\n Phone number : %ld", ptrcontact->li_phoneno);
return;
}
```

