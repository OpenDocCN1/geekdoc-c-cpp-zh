The values recently entered by you are as under
Name : Harshit Jain
E-mail address: harshjain@gmail.com
Phone number: 5412363

In Program 16, the assignment statement ptrcontact=&contact1; would assign the address of the zereth element of structure contact1 to ptrcontact. The members of the structure contact1 are accessed with pointer variable ptrcontact. The arrow operator ($\rightarrow$) is used to access the members. Note that an alternate way (*ptrcontact).c_name can also be used to access members of the structure.

Pointer to a structure can be used to manipulate the values of structure within functions. We have discussed structure passed as a function parameter in Chapter 11. However, if the values of the members of the structure are altered in a function, the change will not be reflected in calling function. If pointer to structure is passed as a parameter, the change will be performed directly on the memory locations, and thus will be reflected in the calling function. Let us write a program and see the usage of pointers to a structure.

Program 17 illustrates the use of pointer to a structure passed as a function parameter.

# $\blacktriangleright$ Program 17

```
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
```