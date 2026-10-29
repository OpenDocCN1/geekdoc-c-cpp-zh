
4. (Practice) a. Write a C++ program that includes the following declaration statements. Have the program use the address operator and a cout statement to display the addresses corresponding to each variable.
int num, count;
long date;
float slope;
double yield;

b. After running the program written for Exercise 4a, draw a diagram of how your computer has set aside storage for the variables in the program. On your diagram, fill in the addresses the program displays.

c. Modify the program written in Exercise 4a (using the sizeof() operator discussed in Section 2.1) to display the amount of storage your computer reserves for each data type. With this information and the address information provided in Exercise 4b, determine whether your computer set aside storage for the variables in the order in which they were declared.

5. (Review) If a variable is declared as a pointer, what must be stored in the variable?

6. (Practice) Using the indirection operator, write expressions for the following:
a. The variable pointed to by xAddr
b. The variable whose address is in yAddr
c. The variable pointed to by ptYld
d. The variable pointed to by ptMiles
e. The variable pointed to by mptr
f. The variable whose address is in pdate
g. The variable pointed to by distPtr
h. The variable pointed to by tabPtr
i. The variable whose address is in hoursPt

7. (Practice) Write declaration statements for the following:
a. The variable pointed to by yAddr is an integer.
b. The variable pointed to by chAddr is a character.
c. The variable pointed to by ptYr is a long integer.
d. The variable pointed to by amt is a double-precision variable.
e. The variable pointed to by z is an integer.
f. The variable pointed to by qp is a single-precision variable.
g. datePt is a pointer to an integer.
h. yldAddr is a pointer to a double-precision variable.
i. amtPt is a pointer to a single-precision variable.
j. ptChr is a pointer to a character variable.

8. (Review) a. What are the variables yAddr, chAddr, ptYr, amt, z, qp, datePt, yldAddr, amtPt, and ptChr used in Exercise 7 called?
b. Why are the variable names amt, z, and qp used in Exercise 7 not good choices for pointer names?

9. (Practice) Write English sentences that describe what's contained in the following declared variables:
a. char *keyAddr;
b. int *m;
c. double *yldAddr;
d. long *yPtr;
e. double *pCou;
f. int *ptDate;

10. (Practice) Which of the following is a declaration for a pointer?
a. long a;
b. char b;
c. char *c;
d. int x;
e. int *p;
f. double w;
g. float *k;
h. float l;
i. double *z;

11. (Practice) For the following declarations,
int *xPt, *yAddr;
long *dtAddr, *ptAddr;
double *ptZ;
int a;
long b;
double c;
determine which of the following statements is valid:
a. yAddr = &a;    b. yAddr = &b;    c. yAddr = &c;
d. yAddr = a;     e. yAddr = b;    f. yAddr = c;
g. dtAddr = &a;   h. dtAddr = &b;  i. dtAddr = &c;
j. dtAddr = a;    k. dtAddr = b;   l. dtAddr = c;
m. ptZ = &a;      n. ptAddr = &b;  o. ptAddr = &c;
p. ptAddr = a;    q. ptAddr = b;   r. ptAddr = c;
s. yAddr = xPt;   t. yAddr = dtAddr;   u. yAddr = ptAddr;

12. (Practice) For the variables and addresses in Figure 8.10, fill in the data determined by the following statements:
a. ptNum = &m;
b. amtAddr = &amt;
c. *zAddr = 25;
d. k = *numAddr;
e. ptDay = zAddr;
f. *ptYr = 2011;
g. *amtAddr = *numAddr;

## 8.2 Array Names as Pointers

Although pointers are simply, by definition, variables used to store addresses, there’s also a direct and close relationship between array names and pointers. This section describes this relationship in detail. Figure 8.11 illustrates the storage of a one-dimensional array named grade, which contains five integers. Each integer requires 4 bytes of storage.

![](img/202cface8244f523c2641baa2e00d7dd_373_0.png)

Using subscripts, the fourth element in the grade array is referred to as grade[3]. The use of a subscript, however, conceals the computer’s extensive use of addresses. Internally, the computer immediately uses the subscript to calculate the array element’s address, based on

![](img/202cface8244f523c2641baa2e00d7dd_373_1.png)

both the array’s starting address and the amount of storage each element uses. Calling the fourth element `grade[3]` forces the compiler to make this address computation:

`&grade[3] = &grade[0] + (3 * sizeof(int))`

Remembering that the address operator (`&`) means “the address of,” this statement is read as “the address of `grade[3]` equals the address of `grade[0]` plus 3 times the size of an integer (which is 12 bytes).” Figure 8.12 shows the address computation used to locate `grade[3]`.

![](img/202cface8244f523c2641baa2e00d7dd_374_0.png)

**Figure 8.12**  Using a subscript to obtain an address

Because a pointer is a variable used to store an address, you can create a pointer to store the address of the first element of an array. Doing so allows you to mimic the computer’s operation in accessing array elements. Before you do this, take a look at Program 8.5.

# Program 8.5

```
#include <iostream>
using namespace std;

int main()
{
    const int ARRAYSIZE = 5;

    int i, grade[ARRAYSIZE] = {98, 87, 92, 79, 85};

    for (i = 0; i < ARRAYSIZE; i++)
        cout << "\\nElement " << i << " is " << grade[i];

    cout << endl;

    return 0;
}
```

When Program 8.5 runs, it produces the following display:

```
Element 0 is 98
Element 1 is 87
Element 2 is 92
Element 3 is 79
Element 4 is 85
```

Program 8.5 displays the values of the grade array by using standard subscript notation. By storing the address of array element 0 in a pointer first, you can use the address in the pointer to access each array element. For example, if you store the address of grade[0] in a pointer named gPtr by using the assignment statement gPtr = &grade[0]; the expression *gPtr (which means "the variable pointed to by gPtr") can be used to access grade[0], as shown in Figure 8.13.

![](img/202cface8244f523c2641baa2e00d7dd_375_0.png)

Figure 8.13 The variable pointed to by *gPtr is grade[0]

One unique feature of pointers is that offsets can be included in expressions using pointers. For example, the 1 in the expression *(gPtr + 1) is an offset. The complete expression references the integer that's one beyond the variable pointed to by gPtr. Similarly, as illustrated in Figure 8.14, the expression *(gPtr + 3) references the variable that's three integers beyond the variable pointed to by gPtr: the variable grade[3].

![](img/202cface8244f523c2641baa2e00d7dd_375_1.png)

Figure 8.14 An offset of 3 from the address in gPtr

Table 8.1 shows the correspondence between elements referenced by subscripts and by pointers and offsets. Figure 8.15 illustrates the relationships listed in this table.

### Table 8.1 Array Elements Can Be Referenced in Two Ways

| Array Element | Subscript Notation | Pointer Notation |
|---|---|---|
| Element 0 | grade[0] | *gPtr or (gPtr + 0) |
| Element 1 | grade[1] | *(gPtr + 1) |
| Element 2 | grade[2] | *(gPtr + 2) |
| Element 3 | grade[3] | *(gPtr + 3) |
| Element 4 | grade[4] | *(gPtr + 4) |

![](img/202cface8244f523c2641baa2e00d7dd_376_0.png)

# Figure 8.15 The relationship between array elements and pointers

Using the correspondence between pointers and subscripts shown in Figure 8.15, the array elements accessed in Program 8.5 with subscripts can now be accessed with pointers, which is done in Program 8.6.

The following display is produced when Program 8.6 runs:

```
Element 0 is 98
Element 1 is 87
Element 2 is 92
Element 3 is 79
Element 4 is 85
```

## Arrays and Pointers

```
Program 8.6

#include <iostream>
using namespace std;

int main()
{
    const int ARRAYSIZE = 5;

    int *gPtr;          // declare a pointer to an int
    int i, grade[ARRAYSIZE] = {98, 87, 92, 79, 85};

    gPtr = &grade[0];        // store the starting array address
    for (i = 0; i < ARRAYSIZE; i++)
        cout << "\nElement " << i << " is " << *(gPtr + i);

    cout << endl;

    return 0;
}
```

Notice that this display is the same as Program 8.5’s display. The method used in Program 8.6 to access array elements simulates how the compiler references array elements internally. The compiler automatically converts any subscript a programmer uses to an equivalent pointer expression. In this case, because the declaration of gPtr includes the information that integers are pointed to, any offset added to the address in gPtr is scaled automatically by the size of an integer. Therefore, *(gPtr + 3), for example, refers to the address of grade[0] plus an offset of 12 bytes (3 × 4), assuming sizeof(int) = 4. This result is the address of grade[3] shown in Figure 8.15.

The parentheses in the expression *(gPtr + 3) are necessary to reference an array element correctly. Omitting the parentheses results in the expression *gPtr + 3. Because of operator precedence, this expression adds 3 to “the variable pointed to by gPtr.” Because gPtr points to grade[0], this expression adds the value of grade[0] and 3 together. Note also that the expression *(gPtr + 3) doesn’t change the address stored in gPtr. After the computer uses the offset to locate the correct variable from the address stored in gPtr, the offset is discarded and the address in gPtr remains unchanged.

Although the pointer gPtr used in Program 8.6 was created specifically to store the grade array’s starting address, doing so is unnecessary. When an array is created, the compiler creates an internal pointer constant for the array and stores the array’s starting address in this pointer. In almost all respects, a pointer constant is identical to a programmer-created pointer variable, but as you’ll see, there are some differences.

For each array created, the array name becomes the name of the pointer constant the compiler creates for the array, and the starting address of the first location reserved for the array
