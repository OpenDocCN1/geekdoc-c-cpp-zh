```
```cpp
amount - value (5000.00,5);        //default for 3rd argument
cout<<"\n Final Value - "<<amount<<"\n\n";

amount - value (10000.00,5,0.30); //pass all arguments explicitly

cout<<"\n Final Value - "<<amount<<"\n\n";

printline('-');                    //use default value for second argument

getch ( );

return 0;
}
float value (float p, int n, float r)
{
    int year - 1; float sum - p;

    while(year<-n)
    {
        sum - sum*(1+r);
        year - year+1;
    }
    return (sum);
}
void printline(char ch, int len)
{
    for (int i-1;i<=len;i++)
        printf("%c",ch);
    printf("\n");
}
```
```

The output of Program 4.2 would be: