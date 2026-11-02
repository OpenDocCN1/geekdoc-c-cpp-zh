
default message is printed. Figure 3 shows the flowchart for this multiple-branch statement.

![](img/d61019b035dd82beb581604273c0ee6b_129_0.png)

Figure 3 Multiple Alternatives

Here you must sort the conditions and test against the largest cutoff first. Suppose we reverse the order of tests:

```
if (richter >= 4.5) // Tests in wrong order
{
    cout << "Damage to poorly constructed buildings";
}
else if (richter >= 6.0)
{
    cout << "Many buildings considerably damaged, some collapse";
}
else if (richter >= 7.0)
{
    cout << "Many buildings destroyed";
}
else if (richter >= 8.0)
{
    cout << "Most structures fall";
}
```

> When using multiple if statements, pay attention to the order of the conditions.

This does not work. Suppose the value of richter is 7.1. That value is at least 4.5, matching the first case. The other tests will never be attempted.

In this example, it is also important that we use a sequence of else if clauses, not just multiple independent if statements. Consider this sequence of independent tests:

```
if (richter >= 8.0) // Didn't use else
{
    cout << "Most structures fall";
}
if (richter >= 7.0)
{
    cout << "Many buildings destroyed";
}
if (richter >= 6.0)
{
    cout << "Many buildings considerably damaged, some collapse";
}
if (richter >= 4.5)
{
    cout << "Damage to poorly constructed buildings";
}
```

Now the alternatives are no longer exclusive. If richter is 7.1, then the last three tests all match, and three messages are printed.

EXAMPLE CODE
See sec03 of your companion code for the full program that prints earthquake descriptions.

## Special Topic 3.3

## The switch Statement

![](img/d61019b035dd82beb581604273c0ee6b_130_0.png)

A sequence of if statements that compares a single integer value against several constant alternatives can be implemented as a switch statement. For example,

```
int digit;
...
switch (digit)
{
    case 1: digitName = "one"; break;
    case 2: digitName = "two"; break;
    case 3: digitName = "three"; break;
    case 4: digitName = "four"; break;
    case 5: digitName = "five"; break;
    case 6: digitName = "six"; break;
    case 7: digitName = "seven"; break;
    case 8: digitName = "eight"; break;
    case 9: digitName = "nine"; break;
    default: digitName = "-"; break;
}
```

![](img/d61019b035dd82beb581604273c0ee6b_130_1.png)

© travelpixpro/iStockphoto

The switch statement lets you choose from a fixed set of alternatives.

## sec04/tax.cpp

```
#include <iostream>
#include <string>

using namespace std;

int main()
{
    const double RATE1 = 0.10;
    const double RATE2 = 0.25;
    const double RATE1_SINGLE_LIMIT = 32000;
    const double RATE1_MARRIED_LIMIT = 64000;

    double tax1 = 0;
    double tax2 = 0;

    double income;
    cout << "Please enter your income: ";
    cin >> income;

    cout << "Please enter s for single, m for married: ";
    string marital_status;
    cin >> marital_status;

    if (marital_status == "s")
    {
        if (income <= RATE1_SINGLE_LIMIT)
        {
            tax1 = RATE1 * income;
        }
        else
        {
            tax1 = RATE1 * RATE1_SINGLE_LIMIT;
            tax2 = RATE2 * (income - RATE1_SINGLE_LIMIT);
        }
    }
    else
    {
        if (income <= RATE1_MARRIED_LIMIT)
        {
            tax1 = RATE1 * income;
        }
        else
        {
            tax1 = RATE1 * RATE1_MARRIED_LIMIT;
            tax2 = RATE2 * (income - RATE1_MARRIED_LIMIT);
        }
    }

    double total_tax = tax1 + tax2;

    cout << "The tax is $" << total_tax << endl;
    return 0;
}
```

### Program Run

Please enter your income: 80000
Please enter s for single, m for married: m
The tax is $10400

![](img/d61019b035dd82beb581604273c0ee6b_134_0.png)

## Common Error 3.4

### The Dangling else Problem

When an if statement is nested inside another if statement, the following error may occur.

```
double shipping_charge = 5.00; // $5 inside continental U.S.
if (country == "USA")
    if (state == "HI")
        shipping_charge = 10.00; // Hawaii is more expensive
    else // Pitfall!
        shipping_charge = 20.00; // As are foreign shipments
```

The indentation level seems to suggest that the else is grouped with the test country == "USA". Unfortunately, that is not the case. The compiler ignores all indentation and matches the else with the preceding if. That is, the code is actually

```
double shipping_charge = 5.00; // $5 inside continental U.S.
if (country == "USA")
    if (state == "HI")
        shipping_charge = 10.00; // Hawaii is more expensive
    else // Pitfall!
        shipping_charge = 20.00; // As are foreign shipments
```

That isn't what you want. You want to group the else with the first if. The ambiguous else is called a dangling else. You can avoid this pitfall if you always use braces, as recommended in Programming Tip 3.2:

```
double shipping_charge = 5.00; // $5 inside continental U.S.
if (country == "USA")
{
    if (state == "HI")
    {
        shipping_charge = 10.00; // Hawaii is more expensive
    }
}
else
{
    shipping_charge = 20.00; // As are foreign shipments
}
```

![](img/d61019b035dd82beb581604273c0ee6b_134_1.png)

## Programming Tip 3.6

### Hand-Tracing

A very useful technique for understanding whether a program works correctly is called hand-tracing. You simulate the program's activity on a sheet of paper. You can use this method with pseudocode or C++ code.

Get an index card, a cocktail napkin, or whatever sheet of paper is within reach. Make a column for each variable. Have the program code ready. Use a marker, such as a paper clip, to mark the current statement. In your mind, execute statements one at a time. Every time the value of a variable changes, cross out the old value and write the new value below the old one.

For example, let's trace the tax program with the data from the program run in Section 3.4.

![](img/d61019b035dd82beb581604273c0ee6b_134_2.png)

Hand-tracing helps you understand whether a program works correctly.

In lines 13 and 14, tax1 and tax2 are initialized to 0.

```
```c
6 int main()
7
8 const double RATE1 = 0.10;
9 const double RATE2 = 0.25;
10 const double SINGLE_LIMIT = 32000;
11 const double MARRIED_LIMIT = 64000;
12
13 double tax1 = 0;
14 double tax2 = 0;
15
```
```

| tax1 | tax2 | income | marital status |
|------|------|--------|----------------|
| 0 | 0 |  |  |
|  |  |  |  |
|  |  |  |  |

In lines 18 and 22, income and marital_status are initialized by input statements.

```
```c
16 double income;
17 cout << "Please enter your income: ";
18 cin >> income;
19
20 cout << "Please enter s for single, m for married: ";
21 string marital_status;
22 cin >> marital_status;
23
```
```

| tax1 | tax2 | income | marital status |
|------|------|--------|----------------|
| 0 | 0 | 80000 | m |
|  |  |  |  |
|  |  |  |  |

Because marital_status is not "s", we move to the else branch of the outer if statement (line 36).

```
```c
24 if (marital_status == "s")
25 {
26   if (income <= SINGLE_LIMIT)
27     tax1 = RATE1 * income;
28   else
29   {
30     tax1 = RATE1 * SINGLE_LIMIT;
31     tax2 = RATE2 * (income - SINGLE_LIMIT);
32   }
33 }
34 else
35
36
37
```
```

Because income is not <= 64000, we move to the else branch of the inner if statement (line 42).

```
```c
38 if (income <= MARRIED_LIMIT)
39 {
40   tax1 = RATE1 * income;
41 }
42 else
43 {
44   tax1 = RATE1 * MARRIED_LIMIT;
45   tax2 = RATE2 * (income - MARRIED_LIMIT);
46 }
```
```

The values of tax1 and tax2 are updated.

```
```c
43 {
44   tax1 = RATE1 * MARRIED_LIMIT;
45   tax2 = RATE2 * (income - MARRIED_LIMIT);
46 }
47 }
```
```

| tax1 | tax2 | income | marital status |
|------|------|--------|----------------|
| β | β | 80000 | m |
| 6400 | 4000 |  |  |

Their sum total_tax is computed and printed. Then the program ends.

```
```c
48
49 double total_tax = tax1 + tax2;
50
51 cout << "The tax is $" << total_tax << endl;
52
53 }
```
```

| tax1 | tax2 | income | marital status | total tax |
|------|------|--------|----------------|-----------|
| β | β | 80000 | m |  |
| 6400 | 4000 |  |  | 10400 |

Because the program trace shows the expected output ($10,400), it successfully demonstrated that this test case works correctly.
