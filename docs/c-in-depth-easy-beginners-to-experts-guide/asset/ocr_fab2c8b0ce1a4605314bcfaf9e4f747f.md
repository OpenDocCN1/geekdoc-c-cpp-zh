# # For eg. it is an error to write:

```
```
Typedef int age a1,a2; /*invalid*/
```
```

# # Typedef using structure:

```
```
typedef struct student
{
    int roll;
    char name[50];
    int marks;
};

main()
{
    st s1,s2;
    or
    struct student s1,s2;
}
```
```

The typedef name can be the same as the tagname of the structure.

# # Typedef and code portability:

The typedef can be used to promote code portability.

Suppose that we have an application that assumes that all integers are represented by 16-bit storage cells. On computer system A, an int may use 32 bits, on another system B may int use 16 bits.

Thus,

```
```
/* on computer system A */
/*integer has 16 bits*/
typedef short int INTEGER;

/*on computer system B*/
/*integer has 32 bits*/
typedef int INTEGER;
```
```

Throughout the program we may use INTEGER instead of short int in the declaration of variables. This typedef could be put in a file such as port.h then included in the files that need integer variables.