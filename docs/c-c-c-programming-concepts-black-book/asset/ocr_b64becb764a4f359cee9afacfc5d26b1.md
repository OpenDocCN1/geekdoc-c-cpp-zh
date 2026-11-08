```
```c
ptr_A = (char*)&var_A;
ptr_B = (char*)&var_B;

printf("\n Address in ptr_A %u",ptr_A);
printf("\n Address of ptr_B %u",ptr_B);

printf("\n Value at ptr_A %d ",*ptr_A);
printf("\n Value at ptr_B %d ",*ptr_B);
return 0;
}
```
```

The preceding code will compile successfully as we have type cast the addresses of integer and float variables to a character pointer. However, we might face problems while displaying the value stored at the given memory location with the help of the * operator, as we have used a char pointer while assigning the address of an integer. In this case, only the information stored in the first byte of memory location is fetched. For the var_A variable, we will get a valid output, as the value stored is 10 and the binary representation of 10 requires only one byte of storage. However, if we change the value to a larger one, which needs more bits for storage in the memory, then we will get a truncated or garbage result. Therefore, if we want to access an integer, then we should store the address in an integer pointer. The same concept applies for the float variable as well.
Next, let's learn how to deal with single dimensional arrays using pointers.

# ## Single Dimensional Arrays using Pointers

An array can be considered as a collection of similar types of elements that are stored in contiguous memory locations. Similar types of elements imply that the variables getting stored could be all int, char, or any other storage class specifier. Following is the syntax for declaring a single dimensional array (also called one-dimensional array):

```
```c
int a[10] ;
```
```

The preceding syntax declares an array of size 10, where each cell in the array is of type int. The size 10 can also be defined as the dimension of array, and the [ ] brackets tell the compiler that the array is being used. As per the C convention, the first element in an array is numbered as 0; therefore, the last element in the array can be found at a location one less than the size of the array. Consider the following example where we have declared and initialized two arrays at the same time:

```
```c
int arr[4] = {1,2,3,4};
int arr[] = {6,7,8,9};
```
```

As shown in the second array, when we declare and define an array at the same time, mentioning the dimension of array becomes optional.

Extra care should be taken while dealing with arrays, as error checks are not done in C to determine whether the subscript used to access the array elements exceeds the size of the array. If the subscript exceeds the size of an array, then the subscript might overwrite its own information on top of some other, which might lead to fatal memory corruption.

Let's now learn how to pass array elements to a function.

Array elements can be passed to a function in two ways: call by value and call by reference. Call by value implies passing the values of array elements to a function; whereas, call by reference implies passing the addresses of array elements to a function. Listing 4.4 shows how to pass the values of array elements to a function:

**Listing 4.4: Passing Values of Array Elements to a Function**

```
```c
#include<stdio.h>
void show_value(int value);
int main()
{
```
```