```
For(i=0;i<3;i++)
For(j=0;j<3;j++)
Scanf("%d",&a[i][j]);
For(i=0;i<3;i++)
For(j=0;j<3;j++)
Scanf("%d",&b[i][j]);
C[i][j]=0;
For(i=0;i<3;i++)
For(j=0;j<3;j++)
{
    C[i][j]=a[i][j]+b[i][j];
    Printf("\n");
}
Printf("%d",c[i][j]);
```

# Multi-Dimensional Arrays

# Declaration

Type array name [s1][s2]....[sm];

Example: int survey[3][5][12];
Float table[5][4][3];

# 4. Define structure and write the general format for declaring and accessing members?

Ans: Structure can store data items in consequent memory locations. The advantage of structures is that the data items may be of different data types.

Declaring structures:

```
Struct student
{
    Char name[20];
    Int stno;
};
```

Memory allocation is as follows:

```
Struct tagname
{
    Data type n1;
    Datatype n2;
};
```

In the case of (1) no memory allocation is not done, only the structure is defined for allocating.