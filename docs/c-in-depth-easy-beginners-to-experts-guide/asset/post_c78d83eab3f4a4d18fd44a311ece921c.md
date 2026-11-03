
There will be no effect in output to change the member in printf().

An object can be assigned to another but can’t be used in other operations.

```c
3 main()
{
    union a
    {
        int i;
        char ch[2];
    };
    union a z=512;
    printf("%d %d",z.ch[0],z.ch[1]);
}
```

Output: 0 2 binary of 512 is (00000010 00000000)

```c
struct emp
{
    char name[20];
    int age;
};
main()
{
    struct emp e = {"matrix", 30};
    f(e);
}
f(struct emp ee)
{
    printf("%s %d",ee.name,ee.age);
}
```

Explanation: Error occurs which can be rectified by declaring the structure before the declaration of the function f().

## Question-What is the similarity between structure, union and enum?

Answer: All of them let us define a new data type.

## Question-Would the following declaration work:

```c
typedef struct s
{
    int a;
    float b;
}s;
```

Answer: Yes

## Question-Can a structure contain a pointer to itself:

Answer: Yes, such structures are known as self referential structures.

## Question-Point out the error if any in the following code

```c
typedef struct
{
    int data;
    NODEPTR link;
}*NODEPTR;
```

Answer: A typedef defines a new name for a type, in this case however the error is that a typedef cannot be used until it is defined. In the given code fragment the typedef declaration is not yet defined at the point where the link field is declared.

## Question: How will you eliminate the above problem?

Answer: To fix this problem, first a name ("struct node") must be given to the structure. Then declare the link field as a simple struct node * as shown below:

```c
typedef struct node
{
    int data;
    struct node *link;
}*NODEPTR;
```

Another way to eliminate the problem is to disentangle the typedef declaration from the structure definition shown below:

```c
struct node
{
    int data;
    struct node *link;
};

typedef struct node *NODEPTR;
```

Yet another way to eliminate the problem is to precede the structure declaration with a typedef, in which case you should use the NODEPTR typedef when declaring the link field as shown below:

```c
typedef struct node *NODEPTR;
struct node
{
    int data;
    NODEPTR link;
};
```

In this case, you declare a new typedef name involving struct node even though struct node has not been completely defined yet; this you are allowed to do.

## Question-

```c
void modify(struct emp*);
struct emp
{
    char name[20];
    int age;
};
main()
{
    struct emp e = {"Sanjay", 35};
    modify(&e);
    printf("%s %d", e.name, e.age);
}
void modify(struct emp *p)
{
    strupr(p->name);
    p->age = p->age + 2;
}
```

Answer: The struct emp is mentioned in the declaration of the function modify() before defining the structure. To solve the problem just declare the function before or after declaration of the structure or just add the statement struct emp before the prototype.

## Question-Would the following code work:

```c
#include<alloc.h>
struct emp
{
    int len;
    char name[1];
};
main()
{
    char newname[] = "Rahul";
    struct emp *p= (struct emp *) malloc(sizeof(struct emp) - 1 +
    strlen(newname)+1);
    p->len=strlen(newname);
    strcpy(p->name, newname);
    printf("%d %s",p->len, p->name);
}
```

Answer: Yes, the program allocates space for the structure with the size adjusted so that the name field can hold the requested name (not just one character as the structure declaration would suggest).

## Question-Can there be a better way to write the above program?

Answer: The best way to implement the problem is to use a character pointer instead of an array as shown below:

```c
#include<alloc.h>
struct emp
{
    int len;
    char *name;
};
main()
{
    char newname[] = "Rahul";
    struct emp *p= (struct emp *) malloc(sizeof(struct emp));
    
    p->len=strlen(newname);
    p->name = malloc(p->len + 1);
    strcpy(p->name, newname);
    printf("%d %s",p->len, p->name);
}
```

Obviously the “convenience” of having the length and the string stored in the same block of memory has now been lost, and freeing instances of this structure require two calls to the function free().

## Question-How would you free the memory allocated in above question?

```c
free(p->name);
free(p);
```

## Question- What would be the output of the following program?

```c
main()
{
    struct emp
    {
        char *n;
        int age;
    };
    struct emp e1 = {"David", 23};
    struct emp e2 = e1;
    strupr(e2.n);
    printf("%s\n", e1.n);
}
```

Answer: David

When a structure is assigned, passed, or returned, the copying is done monolithically. This means that the copies of any pointer fields point to the same place as the original.

In other words, anything pointed to is not copied. Hence, on changing the name through e2.n it automatically changed e1.n

## Question- Point out the error if any in the following code:

```c
main()
{
    struct emp
    {
        char n[20];
        int age;
    };
    struct emp e1 = {"David", 23};
    struct emp e2 = e1;
    if(e1 == e2)
        printf("The structures are equal");
}
```

Structures cannot be compared using the built in == and != operators. This is because there is no single, good way for a compiler to implement structure comparison. A single byte by byte comparison of the bits present in unused paddings in the structure (such padding is used to keep the alignment of later fields correct). A field by field comparison might require unacceptable amounts of repetitive code for large structures. Also, any compiler generated comparison could not be expected to compare pointer fields with strcmp rather than with ==.

## Question- How would you check whether the contents of two structure variables are same or not?

Answer:

```c
struct emp
{
    char n[20];
    int age;
};
main()
{
    struct emp e1 = {"David", 23};
    struct emp e2;
    scanf("%s %d", e2.n, &e2.age);
    if(structcmp(e1, e2) == 0)
        printf("The structures are equal");
    else
        printf("Structures are unequal");
}
structcmp(struct emp x, struct emp y)
{
    if(strcmp(x.n, y.n) == 0)
        if(x.age == y.age)
            return(0);
    return(1);
}
```

In short, if you need to compare two structures, you will have to write your own function to do so which carries out the comparison field by field.

## Question-How are structure passing and returning implemented by the compiler?

Answer: When structures are passed as arguments to functions, the entire structure is typically pushed on the stack. To avoid this overhead many programmers often prefer to pass pointers to structures instead of actual structures. Structures are often returned from functions in a location pointed by an extra, compiler supplied ‘hidden’ argument to the function.

## Question- How can I read/write structures from/to data files?

Answer: To write out a structure we can use fwrite() as shown below:

```c
fwrite(&e, sizeof(e), 1, fp);
```

where e is a structure variable. A corresponding fread() invocation can read the structure back from a file.

On calling fwrite() it writes out sizeof(e) bytes from the address &e. Data files written as memory images with fwrite(), however, will not be portable, particularly if they contain floating point fields or pointers. This is because memory layout of structures is machine and compiler dependent.

Different compilers may use different amount of paddings, and the sizes and byte orders of fundamental types vary across machines. Therefore, structures written as memory images cannot necessarily be read back in by programs running on other machines (or even compiled by other compilers), and this is an important concern if the data files you’re writing will ever be interchanged between machines.

## Question-If the following structure is written to a file using fwrite(), can fread() read it back successfully?

```c
struct emp
{
    char *n;
    int age;
};
struct emp e = {"Sujay", 15};
FILE *fp;
fwrite(&e, sizeof(e), 1, fp);
```

Answer: No, since the structure contains a char pointer while writing the structure to the disk using fwrite() only the value stored in the pointer n would get written (and not the string pointed by it). When this structure is read back the address would be read back but it is quite unlikely that the desired string would be present at this address in memory.

## Question-Would the following program always output the size of the structure as 7 bytes?

```c
struct ex
{
    char ch;
    int i;
    long int a;
};
```

Answer:

No, a compiler may leave holes in structures by padding the first char in the structure with another byte just to ensure that the integer that follows is stored at an even location.
