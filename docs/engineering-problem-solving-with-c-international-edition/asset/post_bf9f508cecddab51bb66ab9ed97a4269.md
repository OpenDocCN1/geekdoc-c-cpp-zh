
data members are name, year, and category. A data member is referenced using the structure variable name followed by a period (called the **structure member operator**) and a data member name. Note the difference between referencing a value in a structure and in an array: A value in an array is referenced with the array name and a subscript.

## Definition and Initialization

To use a structure in a program, you must first define the structure. The keyword `struct` is used to define the name of the structure (also called the structure **tag**) and the data members that are included in the structure. After the structure has been defined, structure variables can be defined using declaration statements. Consider the previous definition for a variable representing a hurricane. The name of the structure is `hurricane`. The three data members are name, year, and category. Note that a semicolon is required after the structure definition.

The statements to define a structure can appear before the `main` function but they are often stored in a header file. It is important to note that these statements do not reserve any memory—they only define the structure. To define a variable of this structure type, we use the following statement in the declaration section of our program:

```
struct hurricane h1;
```

The preceding statement defines a variable named h1 that has three data members; this is shown in the following diagram:

| h1 | ? | name |
|---|---|---|
| | ? | year |
| | ? | category |

The declaration statement allocates memory for the three data members, but initial values have not been assigned; thus, their values are unknown.

The data members of a structure can be initialized in a declaration statement or with program statements. To initialize a structure with a declaration statement, the values are specified in a sequence that is separated by commas and enclosed in braces. The following declaration statement defines and initializes the example structure h1:

```
struct hurricane h1={"Camille", 1969, 5};
```

The data members of h1 are now initialized:

| h1 | "Camille" | name |
|---|---|---|
| | 1969 | year |
| | 5 | category |

To initialize the structure h1 using program statements, we can use statements such as the following:

```
h1.name = "Camille";
h1.year = 1969;
h1.category = 5;
```

Thus, to reference an individual data member, we use the structure variable name and the data member name separated by a period.

## PRACTICE!

Consider the following structure:

```
struct hurricane
{
 char name[10];
 int year, category;
 };
```

Show the contents of the data members of the structures defined in each set of statements.

- 1. struct hurricane h1={"Andrew",1969,5};
- 2. struct hurricane h2;
- 3. struct hurricane h3;
- ...
- h3.name = "Hugo";

## Input and Output

We can use scanf or fscanf statements to read values into the data members of a structure, and printf or fprintf to print the values of the data members. The structure member operator must be used to specify an individual data member. In the next program, the information for a group of hurricanes is read from a file named storms2.txt, and the information is printed to the screen.

![](img/02c4582f051c5b51776411c92b079035_359_0.png)

```
/*
 * Program chapter7_1
 *
 * This program reads the information for a hurricane
 * from a data file and then prints it.
 */
#include <stdio.h>
#define FILENAME "storms2.txt"
/* Define structure to represent a hurricane. */
struct hurricane
{
 char name[10];
 int year, category;
};
int main(void)
{
 /* Declare variables. */
 struct hurricane h1;
 FILE *storms;
/* Read and print information from the file. */
storms = fopen(FILENAME,"r");
if (storms == NULL)
   printf("Error opening data file. \n");
else
{
   while (fscanf(storms,"%s %d %d",h1.name,&h1.year,
                  &h1.category) == 3)
   {
      printf("Hurricane: %s \n",h1.name);
      printf("Year: %d, Category: %d \n",h1.year,
             h1.category);
   }
   fclose(storms);
}
/* Exit program. */
return 0;
}
/*------------------------------------------*/
```

Note that the reference in the fscanf statement for the hurricane name is h1.name instead of &h1.name. Since name is a character string, the variable name represents an address or pointer.

Assume that a sample run of this program contains the information in Table 5.2, page 222. The first few lines would appear as follows:

Hurricane: Hazel
Year: 1954, Category: 4
Hurricane: Audrey
Year: 1957, Category: 4

## PRACTICE!

Assume that the structure variables h1 and h2 have been defined with the following statements:

```
struct hurricane
{
   char name[10];
   int year, category;
};

int main(void)
{
   /* Declare variables. */
   struct hurricane h1={"Audrey",1957,4};
   struct hurricane h2={"Frederic",1979,3};
```

Show the output for each of the following sets of statements.

- 1. printf("%s\n%s \n", h2.name, h1.name);
- 2. printf("Category %d hurricane: %s \n", h1.category, h1.name);

## Computations

We have seen that the structure member operator (.) is used with the name of the structure variable to access individual data members of the structure. When the name of the structure variable is used without the structure member operator, it refers to the entire structure. The assignment operator can be used with the structure variables of the same type to assign an entire structure to another structure, as shown in these statements:

```
struct hurricane
{
   char name[10];
   int year, category;
};

int main(void)
{
   /* Declare variables. */
   struct hurricane h1={"Audrey",1957,4}, h2;

   ...
   h2 = h1;
```

However, relational operators cannot be applied to an entire structure. To compare one structure with another, you must compare the individual data members.

To illustrate computations with structures, consider a program that reads storms2.txt, a file containing hurricane information, and then prints the names of all category 5 hurricanes.

```
/* -------------------------------------------------- */
/*      Program chapter7_2                            */
/*                                                      */
/*      This program reads hurricane information from a data */
/*      file and then prints the names of category 5 hurricanes. */
/*                                                      */

#include <stdio.h>
#define FILENAME "storms2.txt"

/* Define structure to represent a hurricane. */
struct hurricane
{
   char name[10];
   int year, category;
};

int main(void)
{
   /* Declare variables. */
   struct hurricane h1;
   FILE *storms;
/* Read and print information from the file. */
storms = fopen(FILENAME,"r");
if (storms == NULL)
    printf("Error opening data file. \n");
else
{
    printf("Category 5 Hurricanes: \n");
    while (fscanf(storms,"%s %d %d",h1.name,&h1.year,
        &h1.category) == 3)
    if (h1.category == 5)
        printf("%s \n",h1.name);
    fclose(storms);
}
/* Exit program. */
return 0;
}
/*____________________________________________*/
```

## 7.2 Using Functions with Structures

Structures can be used as arguments to functions, and functions can return structures. We will consider each of these cases separately.

## Structures as Function Arguments

Entire structures can be passed as arguments to functions. When a structure is used as a function argument, it is a call-by-value reference. When a function reference is made, the value of each data member of the actual parameter is passed to the function and is used as the value of the corresponding data member of the formal parameter. Thus, changing the value of a formal parameter does not change the corresponding actual parameter. We have modified the program in the previous section. In this chapter, the information for a hurricane is printed from a function.

```
/*---------------------------------------------*/
/* Program chapter7_3                            */
/*                                             */
/* This program reads the information for a hurricane */
/* from a data file and then prints it, using a function. */
/*                                             */
#include <stdio.h>
#define FILENAME "storms2.txt"
/* Define structure to represent a hurricane. */
struct hurricane
{
    char name[10];
    int year, category;
};
int main(void)
{
    /* Declare variables and function prototype. */
    struct hurricane h1;
    FILE *storms;
    void print_hurricane(struct hurricane h);
```
