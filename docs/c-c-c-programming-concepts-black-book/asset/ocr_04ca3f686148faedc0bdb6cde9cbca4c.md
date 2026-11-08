```
Name of the Car -> HYUNDAI
Model of the Car -> SANTRO
Price of the Car -> 40000.000000
Manufacturing Date of the Car -> 22/5/2006
Mileage of the Car -> 15
Name of the Car -> MAHINDRA
Model of the Car -> XYLO
Price of the Car -> 1500000.000000
Manufacturing Date of the Car -> 29/8/2011
Mileage of the Car -> 17
Name of the Car -> MARUTI
Model of the Car -> SX4
Price of the Car -> 1250000.000000
Manufacturing Date of the Car -> 14/9/2010
Mileage of the Car -> 12
Name of the Car -> RENAULT
Model of the Car -> LOGAN
Price of the Car -> 700000.000000
Manufacturing Date of the Car -> 7/7/2006
Mileage of the Car -> 7
```

In the next section, let’s learn about structure variable assignment.

# Assigning a Structure Variable to Another

We can assign a structure variable to another structure variable of the same type. This assignment is done by using the assignment operator (=). When we assign one structure variable to another, we just copy the entire chunk of memory to another variable. It is similar to calling the memcpy() utility function for copying a chunk of memory. In fact, some of the compilers call the same utility when assignments amongst the structure variables take place. A major advantage of using structure assignment is that we are able to directly copy all the content of the structure to another variable. Moreover, there is no need of individual copy members. Listing 5.5 shows how to assign one structure variable to another:

Listing 5.5: Assigning a Structure Variable to Another

```
# include<stdio.h>

struct student
{
                char name[20];
                int class;
                int age;
};
struct student stu1 = {"Tanuman",12,16};
struct student stu2;

int main()
{
        stu2 = stu1; /* Copying Structure variable to another */

        printf("\n Name of student %s",stu2.name);
        printf("\n Class of the student %d",stu2.class);
        printf("\n Age of the student %d",stu2.age);

        getch();
        return 0;
}
```