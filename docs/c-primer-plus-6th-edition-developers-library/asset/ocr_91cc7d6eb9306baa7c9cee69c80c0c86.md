```
ar[index] = (double)rand()/((double) rand() + 0.1);
}

void showarray(const double ar[], int n)
{
    int index;

    for( index = 0; index < n; index++)
    {
        printf("%9.4f ", ar[index]);
        if (index % 6 == 5)
            putchar('\n');
    }
    if (index % 6 != 0)
        putchar('\n');
}

/* sort by increasing value */
int mycomp(const void * p1, const void * p2)
{
    /* need to use pointers to double to access values  */
    const double * a1 = (const double *) p1;
    const double * a2 = (const double *) p2;

    if (*a1 < *a2)
        return -1;
    else if (*a1 == *a2)
        return 0;
    else
        return 1;
}
```

Here is a sample run:

Random list:
    0.0001    1.6475    2.4332    0.0693    0.7268    0.7383
   24.0357    0.1009   87.1828    5.7361    0.6079    0.6330
    1.6058    0.1406    0.5933    1.1943    5.5295    2.2426
    0.8364    2.7127    0.2514    0.9593    8.9635    0.7139
    0.6249    1.6044    0.8649    2.1577    0.5420   15.0123
    1.7931    1.6183    1.9973    2.9333   12.8512    1.3034
    0.3032    1.1406   18.7880    0.9887

Sorted list:
    0.0001    0.0693    0.1009    0.1406    0.2514    0.3032
    0.5420    0.5933    0.6079    0.6249    0.6330    0.7139
    0.7268    0.7383    0.8364    0.8649    0.9593    0.9887