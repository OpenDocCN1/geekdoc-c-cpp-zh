```
```cpp
void main()
{
    int m, n;
    cout<<"Enter any number ";
    cin>>m;
    cout<<" Enter any integer number to calculate power ";
    cin>>n;
    cout<<"power("<<m<<", "<<n<<") = "<<power(m, n);
}
double power(double m, int n)
{
    double d1=m1;
    for(int i=1;i<=n;i++)
    {
        d1 *= m;
    }
    return d1;
}

Output:

Enter any number 5
Enter any integer number to calculate power 4
power(5, 4) = 625
```
```

Q7. Write a program to generate Fibonacci series of a given number by using recursion.

Ans.

```
```cpp
#include<iostream.h>
int fibonacci(int n)
{
    if((n == 1) || (n == 0))
        return 1;
    else
        return fibonacci(n-1) + fibonacci(n-2);
}
void main()
{
    int n;
    cout<<"Enter any integer number :";
    cin>>n;
    cout<<"Fibonacci of "<<n<<" is :"<<fibonacci(n);
}

Output:

Enter any integer number :5
Fibonacci of 5 is :8
```
```