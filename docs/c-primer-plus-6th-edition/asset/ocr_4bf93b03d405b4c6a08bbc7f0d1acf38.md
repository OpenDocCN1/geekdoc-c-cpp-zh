member notation, but passing a pointer means you have to remember to use the indirect membership operator.

+   11. int judge (int (*pf)(const char *));

+   12. a. Note that if ap is an applicant structure, then ap.credit_ratings is an array name and ap.credit_ratings[i] is an array element.

```
void display(applicant ap)
{
    cout << ap.name << endl;
    for (int i = 0; i < 3; i++)
        cout << ap.credit_ratings[i] << endl;
}
```

+   b. Note that if pa is a pointer to an applicant structure, then pa->credit_ratings is an array name and pa->credit_ratings[i] is an array element.

```
void show(const applicant * pa)
{
    cout << pa->name << endl;
    for (int i = 0; i < 3; i++)
        cout << pa->credit_ratings[i] << endl;
}
```

+   13. typedef void (*p_f1)(applicant *);
p_f1 p1 = f1;
typedef const char * (*p_f2)(const applicant *, const applicant *);
p_f2 p2 = f2;
p_f1 ap[5];
p_f2 (*pa)[10];

# Answers to Chapter Review for Chapter 8

+   1. Short, nonrecursive functions that can fit in one line of code are good candidates for inline status.

+   2. a. void song(const char * name, int times = 1);

+   b. None. Only prototypes contain the default value information.

+   c. Yes, provided that you retain the default value for times:
void song(char * name = "O, My Papa", int times = 1);

+   3. You can use either the string "\"" or the character "'" to print a quotation mark. The following functions show both methods:

```
#include <iostream.h>
void iquote(int n)
```