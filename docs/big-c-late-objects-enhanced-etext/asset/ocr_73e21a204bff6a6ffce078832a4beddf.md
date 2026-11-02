```
d. for (int i = 8; i >= 0; i--) { a[i] = a[i + 1]; }
e. for (int i = 1; i < 10; i++) { a[i] = a[i] + a[i - 1]; }
f. for (int i = 1; i < 10; i = i + 2) { a[i] = 0; }
g. for (int i = 0; i < 5; i++) { a[i + 5] = a[i]; }
h. for (int i = 1; i < 5; i++) { a[i] = a[9 - i]; }
```

R6.5 Write a loop that fills an array int values[10] with ten random numbers between 1 and 100. Write code for two nested loops that fill values with ten different random numbers between 1 and 100.

R6.6 Write C++ code for a loop that simultaneously computes both the maximum and minimum of an array.

# R6.7 What is wrong with the following loop?

```
int values[10];
for (int i = 1; i <= 10; i++)
{
    values[i] = i * i;
}
```

Explain two ways of fixing the error.

R6.8 What is an index of an array? What are the legal index values? What is a bounds error?

R6.9 Write a program that contains a bounds error. Run the program. What happens on your computer?

R6.10 Write a loop that reads ten numbers and a second loop that displays them in the opposite order from which they were entered.

R6.11 Trace the flow of the element separator loop in Section 6.2.5 with the given example. Show two columns, one with the value of i and one with the output.

R6.12 Trace the flow of the finding matches loop in Section 6.7.4, where values contains the elements 110 90 100 120 80. Show two columns, for i and matches.

R6.13 Trace the flow of the linear search loop in Section 6.2.7, where values contains the elements 80 90 100 120 110. Show two columns, for pos and found. Repeat the trace when values contains 80 90 100 70.

R6.14 Trace both mechanisms for removing an element described in Section 6.2.8. Use an array values with elements 110 90 100 120 80, and remove the element at index 2.

# R6.15 Consider the following loop for collecting all elements that match a condition; in this case, that the element is larger than 100.

```
vector<double> matches;
for (int i = 0; i < values.size(); i++)
{
    if (values[i] > 100)
    {
        matches.add(values[i]);
    }
}
```

Trace the flow of the loop, where values contains the elements 110 90 100 120 80. Show two columns, for element and matches.