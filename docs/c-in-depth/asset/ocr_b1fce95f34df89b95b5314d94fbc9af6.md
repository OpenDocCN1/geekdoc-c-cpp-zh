and b anywhere in our program. Let us see some examples-

| Expression | | Equivalent |
|---|---|---|
| *p1= 9; | is equivalent to | a = 9; |
| (*p1)++; | is equivalent to | a++; |
| x = *p2 + 10 ; | is equivalent to | x = b + 10; |
| printf("%d %f", *p1, *p2 ); | is equivalent to | printf("%d %f", a, b ); |
| scanf("%d%f", p1, p2 ); | is equivalent to | scanf("%d%f ", &a, &b ); |

The indirection operator can be read as 'value at the address'. For example *p1 can be read as 'value at the address p1'. This indirection operator (*) is different from the asterisk that was used while declaring the pointer variable.

Now we will see what is meant by the term *( &age), where age is a variable. Since &age is an address, so dereferencing it with * operator will give the variable at that address and the variable at that address is age. Hence *( &age) is same as writing age.

```
/*P8.2 Program to dereference pointer variables*/
#include<stdio.h>
main()
{
    int a=87;
    float b=4.5;
    int *p1=&a;
    float *p2=&b;
    printf("Value of p1 = Address of a = %u\n",p1);
    printf("Value of p2 = Address of b = %u\n",p2);
    printf("Address of p1 = %u\n",&p1);
    printf("Address of p2 = %u\n",&p2);
    printf("Value of a = %d %d %d \n",a,*p1,*( &a));
    printf("Value of b = %f %f %f \n",b,*p2,*( &b));
}
```

Output :
Value of p1 = Address of a = 65524
Value of p2 = Address of b = 65520
Address of p1 = 65518
Address of p2 = 65516
Value of a = 87 87 87
Value of b = 4.500000 4.500000 4.500000

We have already seen that while declaring a pointer variable, we have to mention the data type. The reason is that when we use the indirection operator, the number of bytes retrieved will be different for different data types. The value of the pointer only tells the address of starting byte. For example suppose we have a pointer ptr which contains the address 2000 and when we write *ptr the compiler knows that it has to access the information starting at address 2000. So the compiler will look at the base type of the pointer and will retrieve the information depending on that base type. For example if base type is int then 2 bytes information will be retrieved and if base type is float, 4 bytes information will be retrieved and so on. The following figures illustrate this fact. The shaded portion shows the number of bytes retrieved.