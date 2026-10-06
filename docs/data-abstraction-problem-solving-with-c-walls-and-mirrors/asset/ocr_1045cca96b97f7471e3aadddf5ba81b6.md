+   12. What output does the following program produce?

```
int search(int first, int last, int n);
int mystery(int n);

int main()
{
    cout << mystery(30) << endl;
    return 0;
} // end main
int search(int first, int last, int n)
{
    int returnValue = 0;
    cout << "Enter: first = " << first << " last = " << last << endl;\n    int mid = (first + last) / 2;
    if (mid == n) && (n < (mid+1))
        returnValue = mid;
    else if (mid > n)
        returnValue = search(first, mid-1, n);
    else
        returnValue = search(mid+1, last, n);

    cout << "Leave: first = " << first << " last = " << last << endl;\n    return returnValue;
} // end search
int mystery(int n)
{
    return search(n, n, n);
} // end mystery
```

+   13. Consider the following function that converts a decimal number to base 8 and displays the result.

```
void displayOctal(int n)
{
    if (n > 0)
    {
        if (n / 8 > 0)
            displayOctal(n / 8);
        cout << n % 8;
    } // end if
} // end displayOctal
```

Describe how the algorithm works. Trace the function with n = 100.

+   14. Consider the following program:

```
int f(int n)
int main()
{
    cout << "The value of f(8) is " << f(8) << endl;\n    return 0;
} // end main
/* pre n >= 0. */
int f(int n)
{
    cout << "Function entered with n = " << n << endl;\n    switch (n)
```