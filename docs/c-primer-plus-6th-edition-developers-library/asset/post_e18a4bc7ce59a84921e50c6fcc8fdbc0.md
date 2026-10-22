
```
pf1->average = tot / n;
showFlex(pf1);

n = 9;
tot = 0;
pf2 = malloc(sizeof(struct flex) + n * sizeof(double));
pf2->count = n;
for (i = 0; i < n; i++)
{
    pf2->scores[i] = 20.0 - i/2.0;
    tot += pf2->scores[i];
}
pf2->average = tot / n;
showFlex(pf2);
free(pf1);
free(pf2);

return 0;
}
```

```
void showFlex(const struct flex * p)
{
    int i;
    printf("Scores : ");
    for (i = 0; i < p->count; i++)
        printf("%g ", p->scores[i]);
    printf("\nAverage: %g\n", p->average);
}
```

Here is the output:

```
Scores : 20 19 18 17 16
Average: 18
Scores : 20 19.5 19 18.5 18 17.5 17 16.5 16
Average: 18
```

Structures with flexible array members do have some special handling requirements. First, don’t use structure assignment for copying:

```
struct flex * pf1, *pf2; // *pf1 and *pf2 are structures
...
*pf2 = *pf1;  // don't do this
```

This would just copy the nonflexible members of the structure. Instead, use the memcpy() function described in Chapter 16, “The C Preprocessor and the C Library.”

Of course, you could simply have made first and last direct members of person and eliminated nested structures. The anonymous feature becomes more useful with nested unions, which we will discuss later in this chapter.

## Functions Using an Array of Structures

Suppose you have an array of structures that you want to process with a function. The name of an array is a synonym for its address, so it can be passed to a function. Again, the function needs access to the structure template. To show how this works, Listing 14.13 expands our monetary program to two people so that it has an array of two funds structures.

### Listing 14.13 The funds4.c Program

```
/* funds4.c -- passing an array of structures to a function */
#include <stdio.h>
#define FUNDLEN 50
#define N 2

struct funds {
    char  bank[FUNDLEN];
    double bankfund;
    char  save[FUNDLEN];
    double savefund;
};

double sum(const struct funds money[], int n);

int main(void)
{
    struct funds jones[N] = {
        {
            "Garlic-Melon Bank",
            4032.27,
            "Lucky's Savings and Loan",
            8543.94
        },
        {
            "Honest Jack's Bank",
            3620.88,
            "Party Time Savings",
            3802.91
        }
    };

    printf("The Joneses have a total of $%.2f.\n",
```

## Saving the Structure Contents in a File

Because structures can hold a wide variety of information, they are important tools for constructing databases. For example, you could use a structure to hold all the pertinent information about an employee or an auto part. Ultimately, you would want to be able to save this information in, and retrieve it from, a file. A database file could contain an arbitrary number of such data objects. The entire set of information held in a structure is termed a record, and the individual items are fields. Let’s investigate these topics.

What is perhaps the most obvious way to save a record is the least efficient way, and that is to use fprintf(). For example, recall the book structure introduced in Listing 14.1:

```
#define MAXTITL  40
#define MAXAUTL  40
struct book {
    char title[MAXTITL];
    char author[MAXAUTL];
    float value;
};
```

If pbooks identified a file stream, you could save the information in a struct book variable called primer with the following statement:

```
fprintf(pbooks, "%s %s %.2f\n", primer.title,
    primer.author, primer.value);
```

This setup becomes unwieldy for structures with, say, 30 members. Also, it poses a retrieval problem because the program would need some way of telling where one field ends and another begins. This problem can be fixed by using a format with fixed-size fields (for example, "%39s%39s%.2f"), but the awkwardness remains.

A better solution is to use fread() and fwrite() to read and write structure-sized units. Recall that these functions read and write using the same binary representation that the program uses. For example,

```
fwrite(&primer, sizeof (struct book), 1, pbooks);
```

goes to the beginning address of the primer structure and copies all the bytes of the structure to the file associated with pbooks. The sizeof (struct book) term tells the function how large a block to copy, and the 1 indicates that it should copy just one block. The fread() function with the same arguments copies a structure-sized chunk of data from the file to the location pointed to by &primer. In short, these functions read and write one whole record at a time instead of a field at a time.

One drawback to saving data in binary representation is that different systems might use different binary representations, so the data file might not be portable. Even on the same system, different compiler settings could result in different binary layouts.

```
if (ret_val)
{
    find = strchr(st, '\n');    // look for newline
    if (find)                    // if the address is not NULL,
        *find = '\0';            // place a null character there
    else
        while (getchar() != '\n')
            continue;             // dispose of rest of line
}
    return ret_val;
}
```

We’ll look at a couple of sample runs and then discuss the main programming points.

```
$ booksave
Please add new book titles.
Press [enter] at the start of a line to stop.
Metric Merriment
Now enter the author.
Polly Poetica
Now enter the value.
18.99
Enter the next title.
Deadly Farce
Now enter the author.
Dudley Forse
Now enter the value.
15.99
Enter the next title.
[enter]
Here is the list of your books:
Metric Merriment by Polly Poetica: $18.99
Deadly Farce by Dudley Forse: $15.99
Bye.
$ booksave
Current contents of book.dat:
Metric Merriment by Polly Poetica: $18.99
Deadly Farce by Dudley Forse: $15.99
Please add new book titles.
The Third Jar
Now enter the author.
Nellie Nostrum
Now enter the value.
22.99
Enter the next title.
[enter]
Here is the list of your books:
```

## Using Unions

Here is how you can use a union:

```
fit.digit = 23;  // 23 is stored in fit; 2 bytes used
fit.bigfl = 2.0;  // 23 cleared, 2.0 stored; 8 bytes used
fit.letter = 'h'; // 2.0 cleared, h stored; 1 byte used
```

The dot operator shows which data type is being used. Only one value is stored at a time. You can't store a char and an int at the same time, even though there is enough space to do so. It is your responsibility to write the program so that it keeps track of the data type currently being stored in a union.

You can use the -> operator with pointers to unions in the same fashion that you use the operator with pointers to structures:

```
pu = &fit;
x = pu->digit;  // same as x = fit.digit
```

The next sequence shows what not to do:

```
fit.letter = 'A';
inum = 3.02*fit.bigfl;  // ERROR ERROR ERROR
```

This sequence is wrong because a char type is stored, but the next line assumes that the content of fit is a double type.

However, sometimes it can be useful to use one member to place values into a union and to then use a different member for viewing the contents. Listing 15.4 in the next chapter shows an example.

Another place you might use a union is in a structure for which the stored information depends on one of the members. For example, suppose you have a structure representing an automobile. If the automobile is owned by the user, you want a structure member describing the owner. If the automobile is leased, you want the member to describe the leasing company. Then you can do something along the following lines:

```
struct owner {
    char socsecurity[12];
    ...
};

struct leasecompany {
    char name[40];
    char headquarters[40];
    ...
};

union data {
    struct owner owncar;
```

## Summary: Structure and Union Operators

### The Membership Operator:.

**General Comments:**

This operator is used with a structure or union name to specify a member of that structure or union. If name is the name of a structure and member is a member specified by the structure template, the following identifies that member of the structure:

```
name.member
```

The type of name.member is the type specified for member. The membership operator can also be used in the same fashion with unions.

**Example:**

```
struct {
    int code;
    float cost;
} item;
```

```
item.code = 1265;
```

The last statement assigns a value to the code member of the structure item.

### The Indirect Membership Operator:->

**General Comments:**

This operator is used with a pointer to a structure or union to identify a member of that structure or union. Suppose that ptrstr is a pointer to a structure and that member is a member specified by the structure template. Then the statement

```
ptrstr->member
```

identifies that member of the pointed-to structure. The indirect membership operator can be used in the same fashion with unions.

**Example:**

```
struct {
    int code;
    float cost;
} item, * ptrst;
ptrst = &item;
ptrst->code = 3451;
```

The last statement assigns an int value to the code member of item. The following three expressions are equivalent:

```
ptrst->code    item.code    (*ptrst).code
```
