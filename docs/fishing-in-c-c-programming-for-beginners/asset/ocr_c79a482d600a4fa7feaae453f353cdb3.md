# void

Many a times we do not want something to return, at those places we use void as return type. E.g. Consider the following program:

```
#include<iostream>
using namespace std;
void show_prime_status(int);
int main()
{
    int a;
    cout<<"Enter a number\n";
    cin>>a;
    show_prime_status(a);
}
void show_prime_status(int x)
{
    int i;
    for(i=2;i<x;i++)
    if(x%i==0)
    break;
    if(i==x)
    cout<<x<<" is prime";
    else
    cout<<x<<" is not prime";
}
```

Output

Enter a number