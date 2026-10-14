
(One question that comes up is whether the expression `*p++` increments `p` or what it points to. The answer is that it increments `p`. To increment what `p` points to, you can use `(*p)++`.)

When you're doing pointer arithmetic, you have to remember how big the array the pointer points into is, so that you don't ever point outside it. If the array `a` has 10 elements, you can't access `a[50]` or `a[-1]` or even `a[10]` (remember, the valid subscripts for a 10-element array run from 0 to 9). Similarly, if `a` has 10 elements and `ip` points to `a[3]`, you can't compute or access `ip + 10` or `ip - 5`. (There is one special case: you can, in this case, compute, but not access, a pointer to the nonexistent element just beyond the end of the array, which in this case is `&a[10]`. This becomes useful when you're doing pointer comparisons, which we'll look at next.)

### Program 8.2: Program to illustrate the relationship between an array and pointer.

```
#include<stdio.h>

main()

{

int a[10];

int i;

for(i=0;i<10;i++)

scanf("%d",&a[i]);

for(i=0;i<10;i++)

printf("\ni=%d a[i]=%d *(a+i)=%d &a[i]=%u a+i=%u", i, a[i], *(a+i), &a[i], a+i); }

```

Execute this program and observe the result.

### 8.3.2 Pointer Subtraction and Comparison

As we've seen, you can add an integer to a pointer to get a new pointer, pointing somewhere beyond the original (as long as it is in the same array). For example, you might write

```
ip2 = ip1 + 3;
```

Applying a little algebra, you might wonder whether

```
ip2 - ip1 = 3
```

and the answer is, yes. When you subtract two pointers, as long as they point into the same array, the result is the number of elements separating them. You can also ask (again, as long as they point into the same array) whether one pointer is greater or less than another: one pointer is “greater than” another if it points beyond where the other one points. You can also compare pointers for equality and inequality: two pointers are equal if they point to the same variable or to the same cell in an array, and are (obviously) unequal if they don't. (When testing for equality or inequality, the two pointers do not have to point into the same array.)

One common use of pointer comparisons is when copying arrays using pointers.

#### Example 8.3: Here is a code fragment which copies 10 elements from `array1` to `array2`, using pointers. It uses an end pointer, `endptr`, to keep track of when it should stop copying.

```
int array1[10], array2[10];
int *ip1, *ip2 = &array2[0];
int *endptr = &array1[10];
for(ip1 = &array1[0]; ip1 < endptr; ip1++)
*ip2++ = *ip1;
```

As we mentioned, there is no element `array1[10]`, but it is legal to compute a pointer to this (nonexistent) element, as long as we only use it in pointer comparisons like this (that is, as long as we never try to fetch or store the value that it points to.)

### Program 8.3: In the following program, two different pointer variables point to the first and the last element of an integer array.

```
#include<stdio.h>

main()

{

int *px, *py;

int a[5]={1, 2, 3, 4, 5};

px=&a[0];

py=&a[4];

printf("px=%u py=%u", px, py);

printf("\n\n py-px=%u", py-px);

}

```

Execute this program and observe the result.

### 8.3.3 Similarities between Pointers and One-dimensional Arrays

There are a number of similarities between arrays and pointers in C. If you have an array

```
int a[10];
```

you can refer to `a[0]`, `a[1]`, `a[2]`, etc., or to `a[i]` where `i` is an `int`. If you declare a pointer variable `ip` and set it to point to the beginning of an array: `int *ip = &a[0];`
you can refer to `*ip`, `*(ip+1)`, `*(ip+2)`, etc., or to `*(ip+i)` where `i` is an `int`.

There are also differences, of course. You cannot assign two arrays; the code
```
int a[10], b[10];
a = b; /* WRONG */
```
is illegal. As we've seen, though, you can assign two pointer variables:
```
int *ip1, *ip2;
ip1 = &a[0];
ip2 = ip1;
```
Pointer assignment is straightforward; the pointer on the left is simply made to point wherever the pointer on the right does. We haven't copied the data pointed to (there's still just one copy, in the same place); we've just made two pointers point to that one place.

The similarities between arrays and pointers end up being quite useful, and in fact C builds on the similarities, leading to what is called “the equivalence of arrays and pointers in C." When we speak of this “equivalence" we do not mean that arrays and pointers are the same thing (they are in fact quite different), but rather that they can be used in related ways, and that certain operations may be used between them.

The first such operation is that it is possible to (apparently) assign an array to a pointer:
```
int a[10];
int *ip;
ip = a;
```

What can this mean? In that last assignment `ip = a`, C defines the result of this assignment to be that `ip` receives a pointer to the first element of `a`. In other words, it is as if you had written

```
ip = &a[0];
```

The second facet of the equivalence is that you can use the “array subscripting” notation `[i]` on pointers, too. If you write

```
ip[3]
```

it is just as if you had written

```
*(ip + 3)
```

So when you have a pointer that points to a block of memory, such as an array or a part of an array, you can treat that pointer “as if” it were an array, using the convenient `[i]` notation. In other words, at the beginning of this section when we talked about `*ip`, `*(ip+1)`, `*(ip+2)`, and `*(ip+i)`, we could have written `ip[0]`, `ip[1]`, `ip[2]`, and `ip[i]`. As we’ll see, this can be quite useful (or at least convenient).

The third facet of the equivalence (which is actually a more general version of the first one we mentioned) is that whenever you mention the name of an array in a context where the “value” of the array would be needed, C automatically generates a pointer to the first element of the array, as if you had written `&array[0]`. When you write something like

```
int a[10];
int *ip;
ip = a + 3;
```

it is as if you had written

```
ip = &a[0] + 3;
```

which (and you might like to convince yourself of this) gives the same result as if you had written

```
ip = &a[3];
```

For example, if the character array

```
char string[100];
```
