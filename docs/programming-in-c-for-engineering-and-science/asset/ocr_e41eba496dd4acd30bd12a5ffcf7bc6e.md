```
while (j*j < 100)
{
    cout << i + j << endl;
    j *= 2;
}
    i++;
}
cout << "\n*** **\n";
```

```
13. i = 0;
    do
    {
        k = i * i * i - 3 * i + 1;
        cout << i << k << endl;
        i++;
    }
    while (k <= 2);
```

```
14. i = 0;
    do
    {
        j = i * i * i;
        cout << i;
        do
        {
            k = i + 2 * j;
            cout << j << k;
            j += 2;
        }
        while (k <= 10);
        cout << endl;
        i++;
    }
    while (j <= 5);
```

Each of the loops in the following program segment is intended to find the smallest value of number for which the product 1 × 2 × ⋯ × number is greater than limit. For each of Exercises 15–17, make three trace tables, one for each loop, that display the values of number and product for the given value of limit. Assume that number, product, and limit have been declared to be of type int.

```
/* A. Using a while loop */
    number = 0;
    product = 1;
```