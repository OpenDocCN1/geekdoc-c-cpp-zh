element), array operations can be performed easily with pointers. Program 4 illustrates the calculation of address of each array element:

# ▶ **Program 4**

```
/ * Program to illustrate pointer arithmetic and arrays */
#include < stdio . h >

/ * Beginning of function main */
main()
{
/ * Initializing array at compile time */
int i_arr[5]={10,14,12,35,67};

/ * Print address of array elements */
printf(" \n ADDRESS OF ARRAY ELEMENTS \n ");
printf(" \n the address of i_arr[0] is %u", i_arr);
printf(" \n the address of i_arr[1] is %u", i_arr+1);
printf(" \n the address of i_arr[2] is %u", i_arr+2);
printf(" \n the address of i_arr[3] is %u", i_arr+3);
printf(" \n the address of i_arr[4] is %u", i_arr+4);

/ * Print values of array elements */
printf(" \n VALUES OF ARRAY ELEMENTS \n ");
printf(" \n the value of i_arr[0] is %d", *i_arr);
printf(" \n the value of i_arr[1] is %d", *(i_arr+1));
printf(" \n the value of i_arr[2] is %d", *(i_arr+2));
printf(" \n the value of i_arr[3] is %d", *(i_arr+3));
printf(" \n the value of i_arr[4] is %d\n", *(i_arr+4));
return;
}
/ * End of function main */
```

**Output:**

```
ADDRESS OF ARRAY ELEMENTS
The address of i_arr[0] is 65516
The address of i_arr[1] is 65520
The address of i_arr[2] is 65524
The address of i_arr[3] is 65528
The address of i_arr[4] is 65532

VALUE OF ARRAY ELEMENTS
The value of i_arr[0] is 10
The value of i_arr[1] is 14
The value of i_arr[2] is 12
The value of i_arr[3] is 35
The value of i_arr[4] is 67
```

Program 4 can be rewritten as Program 5:

# ▶ **Program 5**

```
/ * Program to illustrate pointer arithmetic and arrays */

#include < stdio . h >
```