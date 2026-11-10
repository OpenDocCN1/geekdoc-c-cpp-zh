[ ], it associates from left to right. For example, in

![](bbox=[0.066, 0.094, 0.452, 0.214])

```
struct myStruct
{
    int a;
    int b;
    int c;
} s1, s2;
```

the first member can be accessed by the construct
s1.a

For any other member of the structure, the construct for accessing it will be similar. Therefore, for assigning a value of 12, say, to the member b of the structure identified by the variable s2, the following statement is written

```
s2.b = 12;
```

To print this value assigned to the member on the screen, the following code is written.

```
printf("%d", s2.b);
```

Similarly, in the preceding example, member b of structure s2 will behave just like a normal variable of type int, although it is referred to as
s2.b

Now, consider the structure given as follows.

```
struct personal_data
{
    char name[100];
    char address[200];
    int year_of_birth;
    int month_of_birth;
    int day_of_birth;
};
```

and the declaration statement for the structure variables monish, venkat, and naresh is given by

```
struct personal_data monish, venkat, naresh;
```

To input the address of monish, the following code is used.

```
scanf("%s", monish.address);
```

The member address of structure personal_data will behave just like a normal array of char. However, it is referred to as monish.address.

In the following example, the year 1982 is assigned to the year_of_birth member of the structure variable monish, of type struct personal_data. Similarly, the month 5 is assigned to the month_of_birth member, and day 4 is assigned to the day_of_birth member. The following statements show the

assignment of the values to the member variables belonging to the structure variable monish.

```
monish.year_of_birth = 1982;
monish.month_of_birth = 5;
monish.day_of_birth = 4;
```

Hence, each member of a structure can be used just like a normal variable, but its name will be a bit longer. Therefore, the ‘dot’ is an operator that separates a member from a structure. This is just one of the ways of accessing any member in a structure. The other two ways will be described in the ensuing sections.

# 14.2.3 Initialization of Structures

A structure can be initialized in much the same way as any other data type. This consists of assigning some constants to the members of the structure. Structures that are not explicitly initialized by the programmer are, by default, initialized by the system. For integer and float data type members, the default value is zero. For char and string type members, the default value is ‘\0’.

The general construct for initializing a structure can be any of the two forms given as follows:

```
struct <structure_tag_name>
{
    <data_type member_name1>;
    <data_type member_name2>;
} <structure_variable1> = {constant1, constant2, . . .};
or
struct <structure_tag_name> <structure_variable>
    = {constant1, constant2, . . .};
```

The following are some examples using both the forms for initialization.

# EXAMPLE

+   5. Initialization of structure using the first construct.

```
#include <stdio.h>
struct tablets
{
    int count;
    float average_weight;
    int m_date, m_month, m_year;
    int ex_date, ex_month, ex_year;
} batch1={2000,25.3,07,11,2004};

int main()
{
    ...
```

![](bbox=[0.572, 0.727, 0.953, 0.922])