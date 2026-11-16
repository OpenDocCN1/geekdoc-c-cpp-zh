The syntax of a union is identical to that of a structure except that the keyword struct is replaced with the keyword union. An example for declaring a union is

```
union exam
{
    int roll_no;
    char name[15];
    int mark1, mark2, mark3;
};
```

In the above example, union exam has 5 members. Second member is a character array name having 15 characters (i.e., 15 bytes). Second member is of type int that requires 2 bytes for their storage. All the other members mark1, mark2, mark3 are integers which requires 2 bytes for their storage. Fig. 2.3 shows the memory allocation of members of union exam.

![](bbox=[0.23, 0.33, 0.75, 0.45])

In the union, all these 5 members are allocated in a common place of memory (i.e., all the members share the same memory location). A union shares the memory space instead of wasting storage on variables that are not being used. The compiler allocates a piece of storage that is large enough to hold the largest type in the union. In the above declaration, the member name requires, 15 characters, which is the maximum of all members, hence a total memory space of 15 bytes is allocated. In case of structures, the total memory space allocated will be 23 (i.e., 15+2+2+2+2) bytes.

# Program 2.12 :

```
/* size.c */
union exam
{
    int roll_no;
    char name[15];
    int mark1, mark2, mark3;
}ul;
/* Union declaration */

struct exam1
{
    int roll_no;
    char name[15];
    int mark1, mark2, mark3;
}s1;
/* Structure declaration */
```