
## Pass by address

Here, when the function is called, the addresses of actual parameters are sent. In the called function, the formal parameters should be declared as pointers with the same type as the actual parameters. The addresses of actual parameter are copied to formal parameter. Using these addresses, the values of the actual parameters can be changed. This way of changing the actual parameters indirectly using its address is called pass by address.

```
/*program to demonstrate pass by address(swapping 2 numbers)*/
#include<stdio.h>

void exchange(int *m,int *n);

void main()
{
    int a=10,b=20;
    exchange(&a,&b);
    printf("a=%d\nb=%d\n",a,b);
}

void exchange(int *m,int *n)
{
    int temp;
    temp=*m;
    *m=*n;
    *n=temp;
}
```

Output:

a=20

b=10

Working:

- Execution starts from main() and variables a and b are assigned 10 and 20 respectively
- The function exchange() is called by sending the address of a and b.
- In function exchange(), the formal parameters m and n declared using * to hold the addresses of a and b
- Using *m and *n we can access the values of a and b and they are exchanged.
- When control comes to the calling function, the values of a and b have been exchanged.

## Recursion

Calling a same function again and again until some termination conditions are satisfied is called recursion. Recursive function should contain base case and general case. While designing recursive function decide about the base case and general case carefully, it should not generate infinite loop.

Base case is a special case where the solution can be obtained without using the recursion. It is also called as terminal condition. Each recursive function must have a base case. A base case serves two purposes:

- It acts as terminating condition
- The recursive function obtains the solution from the base case it reaches.

General case this portion of the code contains the logic required to reduce the size of the problem so as to move towards the base case or terminal condition. Here, each time the function is called, the size of the problem is reduced.

Ex:

```
/*factorial of a number*/

#include<stdio.h>

int fact(int m);

void main()
{
    int n,res;
    printf("enter the number\n");
    scanf("%d",&n);
```

Since array is identified by a common name any element in the array can be accessed by specifying its index or subscript. Index gives the position of an element in the array.

Basic properties of an array are:

- The array elements should be of the same data type.
- The data items stored contiguously in memory
- The subscript of first item is always zero.
- Each data item is accessed using the name of the array, but, with different subscripts.
- The index of the array is always an integer.

## Declaration of single dimensional array

Arrays must be declared and defined before it is used. The declaration informs the compiler about the:

- Type of each element of the array
- Name of the array
- Number of elements (size of an array)

Syntax:

```
Data_typearray_name[int expression];
```

Ex: inta[10];

Here a is an array of 10 integers.

Rules:

- The expression must be enclosed within brackets
- The expression can be an integer constant
- The expression can be an integer expression without variables.

## Initialization of single dimensional arrays

Assigning values to a variable before processing is called initialization. Array elements can be initialized at the time of declaration.

Syntax:

```
Type array_name[expression]={v1,v2,v3,...........vn};
```

Where

- Type can be a data type such as int, float, char etc
- Array_name is the name of the array.
- Expression is an integer and should be enclosed within square brackets.
- v1,v2, are values and should be enclosed within ‘{‘ and ‘}’ separated by commas. The value v1 is stored in 0th location, v2 is stored in 1st location and soon.

The various ways of initializing arrays are:

- Initializing all specified memory locations
- Partial array initialization
- Initialization without size

### Initializing all specified memory locations

Ex:

```
int a[6]={10,15,20,25,30};
```

| 10 | 15 | 20 | 25 | 30 | 35 |
| a[0] | a[1] | a[2] | a[3] | a[4] | a[5] |

### Partial array initialization

If the number of values to be initialized is less than the size of the array, then the elements are initialized in the order from 0th location. The remaining locations will be initialized to zero automatically.

```
int a[5]={10,15};
```

| 10 | 15 | 0 | 0 | 0 |
| a[0] | a[1] | a[2] | a[3] | a[4] |

### Initialization without size

```
int a[]={10,20,30,40,50};
```

| 10 | 20 | 30 | 40 | 50 |
| a[0] | a[1] | a[2] | a[3] | a[4] |

The compiler will calculate the size of the array based on the number of initial values. Here the size is 5.

## Reading/writing single dimensional arrays:

Syntax for reading:

```
for(i=0; i<n; i++)
{
    scanf("%d",&a[i]);
}
```

Where n is the no. of elements of an array.

Syntax for writing:

```
for(i=0; i<n; i++)
{
    printf("%d\n",a[i]);
}
```

Ex:/*program to read n items from the keyboard and display it on the monitor*/

```
#include<stdio.h>

void main()
{
    int a[25],n ,i;
    printf("enter the no. of elements\n");
    scanf("%d",&n);
    for(i=0;i<n;i++)
    {
    scanf("%d",&a[i]);
```

```
printf("enter the no. of elements\n");

scanf("%d",&n);

for(i=0; i<n; i++)
{

scanf("%d",&a[i]);

}

printf("the square of array elements are\n");

for(i=0; i<n; i++)
{

    print_square(a[i]);      /*passing individual array elements*/

}

getch();
}

void print_square(int x)
{

    printf("%d",x*x);

}
```

## Passing the whole array

When passing the whole array to a function,

- The function must be called by passing the name of an array
- In the function definition, the parameter must be declared as an array of the same type as that of actual parameter. No need to specify the size of the array.

Passing whole array to a function is similar to pass by reference. Any change made to the array in the called function will reflect to the original array.

```
/*program to reverse array elements*/

#include<stdio.h>

void reverse(int b[]);

void main()
{
    int a[5]={10,20,30,40,50};
    reverse(a);
    for(i=0; i<5; i++)
    {
        printf("%d\t",a[i]);
    }
}

void reverse(int b[])
{
    b[0]=50, b[1]=40,b[2]=30,b[3]=20,b[4]=10;
}
```

Output:

50 40 30 20 10

Note: in the above program, the parameter b is an array, any change in array b will have the corresponding changes in array a.

## Searching

Process of finding a particular item in the large amount of data is called searching. There are 2 searching techniques.

```
}
}
if(found==1)
    printf("element found at %d position\n",i);
else
    printf("element not found\n");
getch();
}
```

Advantage:

- Very simple approach
- Works well for small arrays
- Used to search when the elements are not sorted

Disadvantage:

- Less efficient if the array size is large
- If the elements are already sorted, linear search is not efficient

**Binary search**: This technique can be applied if the array elements are sorted.

Working:

- Initialize position of the first element to variable low and position of last element to variable high. i.e., **low=0** and **high=n-1**
- Using above initial values obtain the position of middle element as **mid=(low+high)/2**
- The key to be searched is compared with middle element. If the key is same as middle element, then element found and stop searching process. If key is not same as middle element, it may be present in the left part or right part of the array.
- If key is less than the middle element, then left part of the array has to be compared from low to mid-1. So change upper bound as **high=mid-1**
- If key is greater than the middle element, then right part of the array has to be compared from mid+1 to high. So change lower bound as **low=mid+1**
