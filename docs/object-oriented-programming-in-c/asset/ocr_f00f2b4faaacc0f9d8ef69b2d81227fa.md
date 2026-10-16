```
int main()
{
    float amount;

    float value(float p, int n, float r=0.15);  // prototype
    void println(char ch='*', int len=40);      // prototype

    println();                  // uses default values for arguments

    amount = value(5000.00,5);          // default for 3rd argument

    cout << "\n      Final Value = " << amount << "\n\n";

    println('=');       // use default value for 2nd argument

    return 0;
}
/*------------------------------------------------------------*/
float value(float p, int n, float r)
{
    int year = 1;
    float sum = p;

    while(year <= n)
    {
        sum = sum*(1+r);
        year = year+1;
    }
    return(sum);
}

void println(char ch, int len)
{
    for(int i=1; i<=len; i++) printf("%c",ch);
    printf("\n");
}
```

The output of Program 4.2 would be

```
***********************************

    Final Value = 10056.8

===================================
```

Advantages of providing the default arguments are: