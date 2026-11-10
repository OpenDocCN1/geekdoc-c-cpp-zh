
```
int i,j;
p[0] = &a;
p[1] = &b;
p[2] = &c;
p[3] = &d;
p[4] = &e;
p[5] = &f;
p[6] = &g;
p[7] = &h;
p[8] = &k;
p[9] = &l;
display(); /* Displaying the values before
              sorting */
for(i = 0; i < 10; i++)
  for(j = 0; j < 9-i; j++)
    if(*p[j] > *p[j+1])
    {
       temp = p[j];
       p[j] = p[j+1];
       p[j+1] = temp;
    }
display(); /* Displaying after sorting */
return 0;
}
```

This program is very clumsy. It can be rewritten. In the following program, an array of pointers contains the base address of three one-dimensional arrays.

```
{
  int a[]={1,2,3,4,5};
  int b[]={10,20,30,40,50};
  int c[]={100,200,300,400,500};
  int *ap[3]={a,b,c};
  int i;
  for(i=0;i<3;++i)
    printf("%d", *ap[i]);
}
```

In the for loop, printf() prints the values at the addresses stored in ap[0], ap[1], and ap[2], which are 1, 10, and 100.
The above for loop can also be replaced by the following to get the same output.

```
{
  .
  .
  .
  int *p; p=ap;
  for(i=0;i<3;++i)
  {
    printf("%d", *p);
    p++;
  }
}
```

Another illustration is as follows.

```
int main()
{
   int a[3][3]={1,2,3,4,5,6,7,8,9};
   int *ptr[3]={a[0],a[1],a[2]};
   int i;
   for(i=0;i<3;++i)
     printf("%d",*ptr[i]);
   printf("\n");
   for(i=0;i<3;++i)
     printf("%d",*a[i]);
   return 0;
}
```

### Output

```text
1 4 7
1 4 7
```

In the second for loop, the values of the base address stored in the array a[] are printed, which are again 1 4 7.

An array of character pointers that is pointed to the strings is declared as follows.

```
char *nameptr[MAX];
```

The array, nameptr[], is an array of size MAX, and each element of the array is a character pointer. It is then possible to assign character pointer values to the elements of the array. For example,

```
nameptr[1] = "Oxford";
```

The string "Oxford" is placed somewhere in memory by the compiler and the pointer to the string constant is then assigned to nameptr[1]. It is also possible to assign the value of any string pointer to nameptr[1]. For example, if s is a string, then it is possible to assign the pointer value s to nameptr[1].

```
nameptr[1] = s;
```

Again, for example,

```
char *name[] = {"Manas","Pradip","Altaf"};
/* Creates and initializes an array of 3 strings
   name[0] is Manas, name[1] is Pradip and name[2] is Altaf*/
```

Beginners are often confused about the difference between this example and a multidimensional array.

```
char name[3][10] = {"Manas","Pradip","Altaf"};
```

Both of these will behave the same way in most circumstances. The difference can only be seen if we look at the memory locations.

![](img/57923fbb5279ba385cf6b5a2e2c2ea5f_372_0.png)

Fig. 13.11 (a) Logical memory mapping for array of pointers to char (Array of strings)

This instruction increases the pointer so that it points to the next element of the array. If it is followed by the instruction `printf("%d \n", *p);` then it would display the number 2201, which is the content of element `v[1]` (i.e., the second element).

Similarly, we can use instructions such as `++` and `--` to refer to different elements in the array.

![](img/57923fbb5279ba385cf6b5a2e2c2ea5f_375_0.png)

Reference can be made to the different array elements without having to alter the value of p. We have already used `*p` to refer to the first element of the array (or subsequent elements if p has been updated with `++` or `--`), but `*(p+1)` can be used to refer to the next element after `*p`, `*(p+2)` to refer to the one after that, etc.

![](img/57923fbb5279ba385cf6b5a2e2c2ea5f_375_1.png)

Now it is time to turn to the problem of the two-dimensional array. As stated in Chapter 12, C interprets a two-dimensional array as an array of one-dimensional arrays. That being the case, the first element of a two-dimensional array of integers is a one-dimensional array of integers. Moreover, a pointer to a two-dimensional array of integers must be a pointer to that data type. One way of accomplishing this is through the use of the keyword `typedef`. `typedef` assigns a new name to a specified data type.

For example,

```c
typedef unsigned char byte;
```

causes the name `byte` to mean type `unsigned char`. Hence,

```c
byte b[10];
```

would be an array of unsigned characters.

Note that in the `typedef` declaration, the word `byte` has replaced what would normally be the name of `unsigned char`, that is, the rule for using `typedef` is that the new name for the data type is the name used in the definition of the data type. Thus, in

```c
typedef int Array[10];
```

Array becomes a data type for an array of 10 integers. This means that, `Array my_arr;` declares `my_arr` as an array of 10 integers and `Array arr2d[5];` makes `arr2d` an array of five arrays of 10 integers each.

Also note that `Array *ptr2arr;` makes `ptr2arr` a pointer to an array of 10 integers. Because `*ptr2arr` points to the same type as `arr2d`, assigning the address of the two-dimensional array `arr2d` to `ptr2arr`, the pointer to a one-dimensional array of 10 integers is acceptable. Thus, `ptr2arr = &arr2d[0];` or `ptr2arr = arr2d;` are both correct.

Since the data type of the pointer is an array of 10 integers, it is expected that incrementing `ptr2arr` by one would change its value by `10*sizeof(int)`, which it does. Hence, `sizeof(*ptr2arr)` is 20. It can be proved by writing and running a simple short program.

Now, using `typedef` need not necessarily make things clearer for the reader and easier on the programmer. What is needed is a way of declaring a pointer such as `ptr2arr` without using the `typedef` keyword. It turns out that this can be done and that

```c
int(*ptr2arr)[10];
```

is the proper declaration, i.e., `ptr2arr` here is a pointer to an array of 10 integers just as it was under the declaration using the array type. Note that this is different from

```c
int *ptr2arr[10];
```

which would make `ptr2arr` the name of an array of 10 pointers to type `int`.

The elements of a two-dimensional array can be printed using a pointer to an array. The following program illustrates this.

### EXAMPLE

```c
26. int main()
{
    int a[2][3]={{3,4,5},{6,7,8}};
    int i; int(*pa)[3];
    pa=a;
    for(i=0;i<3;++i)
        printf("%d\t",(*pa)[i]);
    printf("\n");
    pa++;
    for(i=0;i<3;++i)
        printf("%d\t",(*pa)[i]);
    return 0;
}
```

### Output

```text
3 4 5
6 7 8
```

**Table 13.7** Difference between an array of pointers and a pointer to an array

| Array of Pointer | Pointer to an Array |
| --- | --- |
| Declaration<br>`data_type *array_name[SIZE];` | Declaration<br>`data_type (*array_name)[SIZE];` |
| Size represents the number of rows | Size represents the number of columns |
| The space for columns may be allotted | The space for rows may be dynamically allotted |

### 13.14 TWO-DIMENSIONAL ARRAYS AND POINTERS

A two-dimensional array in C is treated as a one-dimensional array whose elements are one-dimensional arrays (the rows). For example, a 4 × 3 array of T (where `*T` is any data type supported by C) may be declared by `T a[4][3]`, and described by the following scheme.

Figure 13.12 is the logical layout of a two-dimensional array in memory, but it does not give a good picture of what is happening internally. The ‘internal pseudo-memory map’ works just to display what the two-dimensional array looks like within the system, and can be used to illustrate how it is actually implemented. Figure 13.13 is the graphical representation of a two-dimensional array. Keep in mind that this may not be an accurate picture of what is actually stored in memory, but it is accurate in terms of the concept of a two-dimensional array.

![](img/57923fbb5279ba385cf6b5a2e2c2ea5f_376_0.png)

The first thing to be noticed is that there is still a single pointer that is the name of the entire array, but in this case it is a constant pointer to a constant pointer. It points to an array of pointers, each of which points somewhere inside of the array. Finally, there is the actual storage for the elements of the array. According to the definition of C, all elements of the array must be contiguous. The elements are drawn in the manner shown to emphasize this fact. One may guess, and properly so, that none of the pointers are necessarily real pointers, but are somehow bound up in the addressing logic of the code, or they may be stored in registers. On the other hand, they could actually all be pointers if the implementers decided to do so. There are no assumptions made about the underlying implementation.

The address arithmetic for the `a[n]` array of pointers can be used as done earlier, but it is a slightly different case this time. The following formula is used with size being the number of bytes used to store a pointer.

```
byte_address = a + i * size
```

It will, however, be correct to think of these pointers existing somewhere in memory conceptually in order to understand how a two-dimensional array is stored in the computer memory.

Pointer arithmetic can be performed within each row as is done with the one-dimensional array. The constant pointer named `a[0]` can be considered to be a constant pointer to the first element in the first row and the formula mentioned earlier can be used for pointer arithmetic just as if it were referring to a one-dimensional array. Therefore, the following two expressions,

```
*(a[0] + 3)
```

and

```
a[0][3]
```

are identical as far as the compiler is concerned.

It is possible to keep the first array index set to zero and vary the second array index from zero to eleven, thereby accessing all twelve elements by varying a single subscript. This is considered bad practice in some programming circles.

![](img/57923fbb5279ba385cf6b5a2e2c2ea5f_376_1.png)
