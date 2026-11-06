# Programming Tip 3.6

![](bbox=[0.138, 0.146, 0.259, 0.203])

# Hand-Tracing

A very useful technique for understanding whether a program works correctly is called *hand-tracing*. You simulate the program’s activity on a sheet of paper. You can use this method with pseudocode or C++ code.

Get an index card, a cocktail napkin, or whatever sheet of paper is within reach. Make a column for each variable. Have the program code ready. Use a marker, such as a paper clip, to mark the current statement. In your mind, execute statements one at a time. Every time the value of a variable changes, cross out the old value and write the new value below the old one.

For example, let’s trace the tax program with the data from the program run on page 95. In lines 13 and 14, tax1 and tax2 are initialized to 0.

![](bbox=[0.754, 0.132, 0.923, 0.28])

*Hand-tracing helps you understand whether a program works correctly.*

```
```cpp
6  int main()
7  {
8      const double RATE1 = 0.10;
9      const double RATE2 = 0.25;
10     const double RATE1_SINGLE_LIMIT = 32000;
11     const double RATE1_MARRIED_LIMIT = 64000;
12
13     double tax1 = 0;
14     double tax2 = 0;
15 ```
```

| tax1 | tax2 | income | marital status |
|---|---|---|---|
| 0 | 0 | | |
| | | | |

In lines 18 and 22, income and marital_status are initialized by input statements.

```
```cpp
16     double income;
17     cout << "Please enter your income: ";
18     cin >> income;
19
20     cout << "Please enter s for single, m for married: ";
21     string marital_status;
22     cin >> marital_status;
23 ```
```

| tax1 | tax2 | income | marital status |
|---|---|---|---|
| 0 | 0 | 80000 | m |
| | | | |

Because marital_status is not "s", we move to the else branch of the outer if statement (line 36).

```
```cpp
24     if (marital_status == "s")
25     {
26         if (income <= RATE1_SINGLE_LIMIT)
27         {
28             tax1 = RATE1 * income;
29         }
30         else
31         {
32             tax1 = RATE1 * RATE1_SINGLE_LIMIT;
33             tax2 = RATE2 * (income - RATE1_SINGLE_LIMIT);
34         }
35     }
36     else
37     {
```
```

Since income is not <= 64000, we move to the else branch of the inner if statement (line 42).

```
```cpp
38         if (income <= RATE1_MARRIED_LIMIT)
39         {
40             tax1 = RATE1 * income;
41         }
42         else
43         {
44             tax1 = RATE1 * RATE1_MARRIED_LIMIT;
45             tax2 = RATE2 * (income - RATE1_MARRIED_LIMIT);
46         }
```
```