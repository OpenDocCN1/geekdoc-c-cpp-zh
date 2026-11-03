```
}res;
res.marks=90;
printf("Marks : %d\n",res.marks);
res.grade='A';
printf("Grade : %c\n",res.grade);
res.per=85.5;
printf("Percentage : %f\n",res.per);
}
```

# Output :

Marks : 90
Grade : A
Percentage : 85.500000

Before the first printf, the value 90 is assigned to the union member marks, so other members grad and per contain garbage value. After first printf, the value 'A' is assigned to the union member grad So now the other two members marks and per contain garbage value. Only one member of union ca hold value at a time, don't try to use all the members simultaneously. So a union variable of type resu can be treated as either an int variable or char variable or a float variable. It is the responsibility the programmer to keep track of member that currently holds the value.

Union variables can also be initialized, but there is a limitation. We know that due to sharing of memor all the members can't hold values simultaneously. So during initialization also only one member can given an initial value, and this privilege is given to the first member. Hence only the first member a union can be given an initial value. The type of the initializer should match with the type of the fi member. For example, we can initialize the above union variable as-

```
union result res ={78};
```

Now we'll take a program and compare the memory allocated for a union and structure variable

```
/* P10.17 Program to compare the memory allocated for a union and structu variable*/
#include<stdio.h>
struct stag{
    char c;
    int i;
    float f;
};
union utag{
    char c;
    int i;
    float f;
};
main()
{
    union utag uvar;
    struct stag svar;
    printf("Size of svar = %u\n",sizeof(svar));
    printf("Address of svar : %u\t",&svar);
    printf("Address of members : %u %u %u\n",&svar.c,&svar.i,&svar.
    printf("Size of uvar = %u\n",sizeof(uvar));
```