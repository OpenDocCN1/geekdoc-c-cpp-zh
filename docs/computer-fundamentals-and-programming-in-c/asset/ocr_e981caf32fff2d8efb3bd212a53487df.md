```
printf("nValue of * (&i) = %d", *(&i));
```

Output

```
value of i = 5
value of * (&i) = 5
```

Note that printing the value of *(&i) is same as printing the value of i. * always implies value at address. *(&i) is identical to i. The unary operators & and * bind more tightly than arithmetic operators; they associate right to left, hence *&i is equivalent to *(&i).

The placement of the indirection operator before a pointer is said to dereference the pointer. The value of a dereferenced pointer is not an address, but rather the value at that address—that is, the value of the variable that the pointer points to.

For example, in the preceding program, iPtr's value is the address of num. However, the value of iPtr dereferenced is the value of num. Thus, the following two statements have the same effect, both changing the value of num.

```
num = 25;
*iPtr = 25;
```

Similarly, a dereferenced pointer can be used in arithmetic expressions in the same fashion as the variable to which it points. Thus, the following two statements have the same effect.

```
num *= 2;
*iPtr *= 2;
```

In these examples, changing a variable's value using the indirection operator rather than through a straightforward assignment seems like an unnecessary complication. However, there are instances (discussed later in this chapter), such as looping through an array using a pointer, or using dynamic memory allocation, in which using the indirection operator is helpful or even necessary.

+   Note
+   
+   - Address of operator (&): It is used as a variable prefix and can be translated as 'address of'. Thus, &variable can be read as address of variable.
+   - Dereference operator (*): It can be translated by 'value pointed by' or value at address'. 'ptr can be read as 'value pointed by ptr'. It indicates that what has to be evaluated is the content pointed by the expression considered as an address.

The following example shows how pointers can be used to add numbers given by the user through the use of pointers without using the variable directly.

```
#include <stdio.h>
int main()
{
    int a,b,c;
    int *pa,*pb,*pc;
    pa=&a;
    pb=&b;
```

```
pc=&c;
printf("\n ENTER THE FIRST NUMBER:");
scanf("%d",pa);
printf("\n ENTER THE SECOND NUMBER:");
scanf("%d",pb);
*pc=*pa+*pb;
printf("\n SUM IS %d",*pc);
return 0;
}
```

Output

```
ENTER THE FIRST NUMBER 5
ENTER THE SECOND NUMBER 6
SUM IS 11
```

The following statements are also valid.

```
*ptr = *ptr + 10;
```

increments *ptr by 10. The unary operators * and & bind more tightly than arithmetic operators, so the assignment

```
y = *ptr + 1
```

takes whatever ptr points at, adds 1, and assigns the result to y, while

```
*ip += 1
```

increments what ptr points to. A pointer variable does not always points to a particular variable throughout the program. It can point to any variable; the only precondition is that its type must be same because the pointer variable is bound to specific data type. The following program illustrates this fact.

```
#include <stdio.h>
int main()
{
    int a=5, b=10;
    int *p;
    p = &a;
    printf("\na=%d b=%d *p=%d", a, b,*p);
    p=&b;
    printf("\na=%d b=%d *p=%d", a, b,*p);
    return 0;
}
```

Output

```
a=5 b=10 *p=5
a=5 b=10 *p=10
```

# 13.5 VOID POINTER

A void pointer is a special type of pointer. It can point to any data type, from an integer value or a float to a string of characters. Its sole limitation is that the pointed data cannot be referenced directly (the asterisk * operator cannot be used on them) since its length is always undetermined. Therefore, type casting or assignment must be used to turn the void pointer to a pointer of a concrete data type to which we can refer. Take a look at the following example.

```
#include <stdio.h>
int main()
```