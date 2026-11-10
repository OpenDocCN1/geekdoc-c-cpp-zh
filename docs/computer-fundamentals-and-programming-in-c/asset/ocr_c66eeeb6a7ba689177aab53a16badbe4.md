member. Enumeration data types are data items whose values may be any member of a symbolically declared set of values. Bitfields are identifiers

whose bit-width can be specified and used to form packed words containing different fields.

# ## KEY TERMS

**Accessing a structure member**  It refers to the act of handling any member of a structure for the purpose of assigning a value or using the member in any expression.

**Arrays of structures**  It refers to that “structure variable” which is an array of objects, each of which contains the member elements declared within the structure construct.

**Initialization of structure**  It refers to assigning values to members of an instance variable.

**Instance variable**  It is one of the named pieces of data that make up a structure.

**Non-homogeneous data**  It includes data of different types such as integer, float, character, etc.

**Structure**  It is a collection of data grouped together and treated as a single object.

**Type template**  It is a document or file having a preset format, used as a starting point for a particular application so that the format does not have to be recreated each time it is used.

# ## FREQUENTLY ASKED QUESTIONS

+   1. **What is the difference between structure and union?**
+   
+   **Memory allocation** The amount of memory required to store a structure is greater or equal to the sum of the size of all the members in addition to the slack bytes or padding bytes that may be provided by the compiler. On the other hand, in case of a union, the amount of the memory required is same as that of the largest member.
+   
+   **Member Access** While all structure members can be accessed at any point of time, only one member of a union can be accessed at any given time. Because at a particular moment of time, only one union member will have a meaningful value. The other members have garbage values.
+   
+   **Identifying active members** There is no way to find which of the members is active at any moment of time. The program must keep track of active members explicitly.

+   2. **Why can’t structures be compared?**
+   
+   These can be unused padding bytes with structures as needed by alignment requirements for a platform and how they are filled is not defined by the standard. Hence, a byte by byte comparison will also fail. This is because the comparison might stumble on random bits present in unused “holes” in the structure as padding is used to keep the alignment of the latter fields correct. So, a memcmp() of the two structure will almost never work.

+   3. **How can two structures be compared?**
+   
+   One way to compare two structures is comparing the individual fields in the structure.

+   4. **Why do structures get padded?**
+   
+   Almost all modern processors support byte addressing, i.e. an address is the address of a byte. However, there is often a constraint that larger data items (integers and floating-point numbers) should start at locations whose address is a multiple of the size of the data item. This constraint called, an alignment constraint, much simplifies the handling of such data items. Structure padding occurs because the members of the structure must appear at the correct byte boundary. This enables the CPU to access the members faster. If they are not aligned to word boundaries, then accessing them might take up more time. So the padding results in faster access.
+   
+   Additionally, the size of the structure must be such that in an array of the structures all the structures are correctly aligned in memory, so there may be padding bytes (also known as slack bytes) at the end of the structure too.

+   5. **How can the effect of padding be minimized?**
+   
+   Structure padding definitely introduces unused holes. There is no standard method to control the padding of structure. One suggested way may be to

arrange the members in the order of their largest to the smallest sizes.

+   6. **While compiling a program the following error message “Floating point formats not linked is obtained”. What is wrong with the program?**
+   
+   When parsing the source file, if the compiler encounters a reference to the address of a float, it sets a flag to have the linker link in the floating point emulator. A floating point emulator is used to manipulate floating point numbers in run time of library functions like scanf() and atof() etc.
+   
+   There are some cases in which the reference to the float does not necessitate the compiler to involve the emulator. The most common case is the one which uses scanf() to read a float in an array of structures and does not call any other functions related with floating point manipulation. In such cases the run time error might be caused by giving the message “Floating point formats not linked”.
+   
+   The solution of this problem is that the emulator will be used in such a fashion that the compiler can accurately determine when to link in the emulator. To force the floating point emulator to be linked into an application, just include the following functions in your program.

```
~~~c
void FloatLink()
{
    float a = 0 , *b = &a;
    a = *b;
}
Or
static void forcefloat (float *p)
{
    float f=*p;
    forcefloat(&f);
}
~~~
```

There is no need to call these functions; but it is necessary to include it anywhere in the program.

Another solution is to include the following statements at the beginning of the program.

```
~~~c
#include <math.h>
double dummy = sin(0.0);
~~~
```

This code forces the compiler to load the floating-point version of scanf().