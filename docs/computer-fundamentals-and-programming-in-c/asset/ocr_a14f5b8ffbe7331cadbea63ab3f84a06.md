```
~~~c
printf("\n r = %7.2f",r);
return 0;
}
~~~
```

**Output**

p = 48.56
q = 458.66
r = 0

12. A railway ticket generation program that uses named initialization in a structure.

```
~~~c
#include<stdio.h>
struct traveler
{
    int class;
    char train_num[40];
    char coach_num[6];
    int seat_num;
    char from[30];
    char to[30];
    char gender[10];
    int age;
    int dep_date[10];
    char name[80];
};
struct traveler passenger8 =
{
    .name = "JIT SINHA",
    .to = "Jaipur",
    .from = "Raigarh",
    .train_num = "superfast 154",
    .dep_date[0] = 30,
    .dep_date[1] = 8,
    .dep_date[2] = 2010,
    .gender = "M",
    .age = 28,
    .class = 1
};
int main()
{
    printf("\n enter coach number:");
    scanf("%s",&passenger8.coach_num);
    printf("\n enter seat number:");
    scanf("%d", &passenger8.seat_num);
    printf("\nxxxxxxxxx Ticket xxxxxxxxxx");
    printf("\n\n\n Name of Ticket holder : %s", passenger8.name);
    printf("\n\n Train : %s:",passenger8.train_num);
~~~
```

```
~~~c
    printf("\n\n From : %s, Date of Departure:", passenger8.from);
    for(int i=0;i<3;i++)
        printf(" :%d ",passenger8.dep_date[i]);
    printf("\n\n To: %s", passenger8.to);
    printf("\n\n Coach No.: %s Seat No.:%d",passenger8.coach_num,passenger8.seat_num);
    printf("\n\nxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx");
    return 0;
}
~~~
```

**Output**

enter coach number: 56
enter seat number: 41
xxxxxxxxxxxxxx Ticket xxxxxxxxxxxxxx
Name of Ticket holder : JIT SINHA
Train : Superfast 154:
From : Raigarh, Date of Departure : : 30 : 8 : : 2010 :
To: Jaipur
Coach No.: 56  Seat No.: 41

# ### 14.2.4 Copying and Comparing Structures

A structure can be assigned to another structure of the same type. Here is an example of assigning one structure to another.

**EXAMPLE**

13. Copying one structure to another of the same type.

```
~~~c
#include <stdio.h>
struct employee
{
    char grade;
    int basic;
    float allowance;
};
int main()
{
    struct employee ramesh={'b', 6500, 812.5};
                    /* member of employee */
    struct employee vivek;
                    /* member of employee */
    vivek = ramesh; /* copy respective members of
                       ramesh to vivek */
    printf("\n vivek's grade is %c, basic is Rs %d, \n allowance is Rs %f", vivek.grade,vivek.basic,
           vivek.allowance);
    return 0;
}
~~~
```

**Output**

vivek's grade is b, basic is Rs 6500, allowance
is Rs 812.500000