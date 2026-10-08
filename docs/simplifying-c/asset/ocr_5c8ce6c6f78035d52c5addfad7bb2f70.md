```
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
Enter first number: 7
The sum of two integers 6 and 7 is 13
```

The function add in Program 15 accepts two parameters; it then performs addition operation on the values accepted and then returns the result. In function main, the statement int (*funp_add) (int, int) declares a function pointer named funp_add that can store the address of the function, which can accept two integer parameters and returns an integer value.

During the execution of Program 15, the variable funp_add is assigned the address of the function add using the statement funp_add=add:. Then a call is made to function add through the statement i_ans = (*funp_add)(i_first, i_second):. The result returned by function is assigned to i_ans variable and it is displayed on the screen with printf() function.

# 12.7 Pointers and Structures

We have discussed that the name of an array acts as a pointer to an array. Similar is the case with structures. The name of the structure can act as a pointer to the entire structure. Thus, each member of a structure can be accessed using the name of the structure. However, the way array members were accessed and the way structure members are accessed are quite different. The reason behind it is structure members are of different data types, and thus, the storage space occupied by each member is different. Therefore, the pointer arithmetic calculations used with arrays will not work with structures. Pointer to structure can be declared similar to other pointer variables. For instance, to define prccontact as pointer to structure, prccontact is to be preceded by the * symbol:

```
struct contact
{
char c_name[30];

unsigned long int li_phoneno;
```