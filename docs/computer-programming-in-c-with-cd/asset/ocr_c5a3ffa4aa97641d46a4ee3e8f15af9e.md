```
```cpp
result=0;
}
void gcd :: gcdinput()
{
    cout<<"Enter First number";
    cin>> m;
    cout<<"Enter second number";
    cin>>n;
}
void gcd :: gcdcompute()
{
    int Remainder;
    int max, min;
    max=m > n ? m:n;
    min=m<n ? m:n;

    while (min!=0)
    {
        Remainder =max % min;
        max=min;
        min=Remainder;
    }

    result=max;

}
void gcd :: gcdoutput()
{
    cout<<" The gcd of two numbers is:";
    cout<< result << endl;
}

void main()
{
    gcd g;

    g.gcdinput();
    g.gcdcompute();
    g.gcdoutput();

}
```
```