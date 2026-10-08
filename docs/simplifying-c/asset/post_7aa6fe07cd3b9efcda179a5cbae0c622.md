
int *large(int *, int *);
/* Beginning of function main */
main()
{
/* Declare variables */
int i_first, i_second, *i_large;

/* Accept values */
printf("\n Enter the values of number 1 and number 2 : ");
scanf("%d %d", &i_first, &i_second);

/* Function call large */
i_large = large(&i_first, &i_second);
/* Display larger of two numbers */
printf("\n the larger number is %d\n", *i_large);
return;
}
/* End of function main */

/* Function returning pointer to an integer */
/* Beginning of function large */
int *large(int *i_first, int *i_second)
{
if (*i_first > *i_second)
return i_first;
else
return i_second;
}

/* End of function large */

# Output:

Enter the values of number 1 and number 2 : 40 10
The larger number is 40

Program 14 contains a function named large that accepts two parameters. Both the parameters passed by calling function are addresses, and thus, the pointers are used to accept these addresses. The large function finalizes the larger of the two numbers and returns the address of the variable that contains larger value. Thus, to accept address returned, the pointer variable i_large is used in calling function. Observe that in the prototype of function large, we have used the statement int *large(int *, int *). The * prefixed to the function name large here indicates that the value returned by the function is a pointer to an integer. Note that the functions can return address of variables defined in a calling function. An error will be encountered if the function returns address of variable defined locally in a function.

## Function Pointer

We know that pointer can point to any standard C data types such as integer, float, or character. The array name when used in expression gives address of the first element of array. Similarly, the name of the function represents its starting address. Thus, we can also define a pointer that points to a function. Once defined, such a pointer can be used to invoke a function. The syntax for declaring a function pointer is as follows:

```
data type (*func_pointer)( data type of function parameters);
```

where func_pointer is a variable name that can hold address of an function. The asterisk (*) operator precedes the function pointer variable. The declaration of function pointer also includes data type of parameters the function will accept along with the data type of the value a function will return. To declare a function pointer that points to function exchange written in Program 13, the following syntax is used:

```
void (*funp_exchange) (int *, int *);
```

where *funp_exchange is the pointer variable that stores address of function that accepts two pointer variables as parameter and does not return any value.

Note that the term *funp_exchange is written within brackets. The use of brackets here is important as it differentiates between a function pointer and function returning a pointer value. If the preceding definition is modified as void *funp_exchange (int *, int *);, then this definition refers to function named funp_exchange that accepts two pointer variables and returns a void pointer. Hence, the user has to be cautious when using function pointers. Program 15 illustrates the use of function pointer:

## Program 15

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

**Output:**

```
Enter first number: 6
Enter second number: 7
The sum of two integers 6 and 7 is 13
```

The function add in Program 15 accepts two parameters; it then performs addition operation on the values accepted and then returns the result. In function main, the statement int (*funp_add) (int, int) declares a function pointer named funp_add that can store the address of the function, which can accept two integer parameters and returns an integer value.

During the execution of Program 15, the variable funp_add is assigned the address of the function add using the statement funp_add=add. Then a call is made to function add through the statement i_ans = (*funp_add)(i_first, i_second). The result returned by function is assigned to i_ans variable and it is displayed on the screen with printf() function.

## 12.7 Pointers and Structures

We have discussed that the name of an array acts as a pointer to an array. Similar is the case with structures. The name of the structure can act as a pointer to the entire structure. Thus, each member of a structure can be accessed using the name of the structure. However, the way array members were accessed and the way structure members are accessed are quite different. The reason behind it is structure members are of different data types, and thus, the storage space occupied by each member is different. Therefore, the pointer arithmetic calculations used with arrays will not work with structures. Pointer to structure can be declared similar to other pointer variables. For instance, to define ptrcontact as pointer to structure, ptrcontact is to be preceded by the * symbol:

```
struct contact
{
char c_name[30];

unsigned long int li_phoneno;
char c_email[50];
} *ptrcontact, contact1;

ptrcontact= contact1;
```

The difference observed in the usage of normal structures and pointer structures is the way the variables are accessed. The dot (. ) operator is used to access individual members of the structures as discussed in Chapter 11. However, to access structure members with pointer to a structure, arrow (->) operator is used. For example, to scan the value of c_name, scanf("%[^
]", ptrcontact->c_name) will be used. Let us write a program to understand how pointer to a structure works. Program 16 illustrates the usage of pointer to structure.

## Program 16

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

**Output:**

Enter name : Harshit Jain

Enter e-mail address: harshjain@gmail.com

Enter phone number: 5412363

The values recently entered by you are as under
Name : Harshit Jain
E-mail address: harshjain@gmail.com
Phone number: 5412363

In Program 16, the assignment statement ptrcontact=&contact1; would assign the address of the zeroth element of structure contact1 to ptrcontact. The members of the structure contact1 are accessed with pointer variable ptrcontact. The arrow operator (->) is used to access the members. Note that an alternate way (*ptrcontact).c_name can also be used to access members of the structure.

Pointer to a structure can be used to manipulate the values of structure within functions. We have discussed structure passed as a function parameter in Chapter 11. However, if the values of the members of the structure are altered in a function, the change will not be reflected in calling function. If pointer to structure is passed as a parameter, the change will be performed directly on the memory locations, and thus will be reflected in the calling function. Let us write a program and see the usage of pointers to a structure.

Program 17 illustrates the use of pointer to a structure passed as a function parameter.

## Program 17

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
