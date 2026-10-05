# Answers to Self-Test Exercises

+   1. Hip Hurray
2. using std::cout;

```
void stars(int n)
{
    cout << '*';
    if (n > 1)
        stars(n - 1);
}
```

The following is also correct, but is more complicated:

```
void stars(int n)
{
    if (n <= 1)
    {
        cout << '*';
    }
    else
    {
        stars(n - 1);
        cout << '*';
    }
}
```

+   3. using std::cout;

```
void backward(int n)
{
    if (n < 10)
    {
        cout << n;
    }
    else
    {
        cout << (n%10);//write last digit
        backward(n/10);//write the other digits backward
    }
}
```

+   4. The answer to Self-Test Exercise 4 is writeUp. The answer to Self-Test Exercise 5 is writeDown.,

```
#include<iostream>
using std::cout;
using std::endl;
```