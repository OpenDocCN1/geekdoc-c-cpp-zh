```
void main()
{
    struct class_room_1 s1 = ("Jeyabal", 876543);
    struct class_room_1 s2 = ("Vanitha");
    printf("Name is %s", s1.name);
    printf("\nReg no is %d", s1.reg_no);
    printf("\n\nName is %s", s2.name);
    printf("\nReg no is %d", s2.reg_no);
    s3 = s1;
    printf("\n\nnName is %s", s3.name);
    printf("\nnReg no is %d", s3.reg_no);
}
```

> The program displays the following output
> Name is Jayabal
> Reg no is 876543
> Name is Vanitha
> Reg no is 0
> Name is Jayabal
> Reg no is 876543

Program 2.10 shows an example for initializing the structure using the structure name. The values to be initialized for the members of a structure must be enclosed within a pair of braces. Note that the constants to be initialized to the members of the structure must be in the same order in which the members are declared in the structure. If some of the structure members are not initialized, then the C compiler will automatically initialize them to zero. This is what you get for the structure variable s2 in Program 2.10.

The information contained in one structure variable can also be assigned to another structure variable using a single assignment statement. In Program 2.10 we have used,

```
s3 = s1;
```

to copy the values in structure variable s1 to s3. This type of assignment statements will be necessary when many members of the structure are to be initialized. Note that one structure variable can be assigned to another only when they both are of the same structure type.