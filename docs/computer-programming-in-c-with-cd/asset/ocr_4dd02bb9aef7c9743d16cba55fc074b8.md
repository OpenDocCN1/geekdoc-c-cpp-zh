Q30: What do you mean by function overloading? Write C++ program to perform addition of two integer number and three floating point number using function name add() but with different number and type of argument (Mumbai University, May 2009)

Ans:

```
```cpp
#include<iostream.h>

void add(int a, int b, int &sum)
{
sum=a+b;
}

void add (float a, float b, float c, float &sum)
{
sum=a+b+c;
}
```
```

Q31: What do you mean by Constructor? Write a C++ program to generate first ‘n’ terms of Fibonacci series using constructor function. (Mumbai University, May 2009)

Ans:

```
```cpp
# include<iostream.h>

class fibbo
{
    public:

    fibbo()
    {

        int F1=1;
        int F2=1;
        int n;
        cout<<"\n Enter No. of terms generated";
        cin>>n;
        cout<<"  "<<F1<<"   "<<F2;
        for (int i=3; i<=n; i++)
        // this segment generates 3rd term on words
        {
                int F= F1+F2;
                cout<<"  "<<F;
```
```