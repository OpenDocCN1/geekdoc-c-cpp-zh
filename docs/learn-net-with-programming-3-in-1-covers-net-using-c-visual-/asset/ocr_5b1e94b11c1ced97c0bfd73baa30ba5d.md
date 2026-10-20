Int mymethod(int x)

Float mymethod(float x)

Double mymethod(double x, double y)

Consider the following Example:, which have two methods that add numbers of different type:

# Example:

```
Static int plusmethodint(int x, int y)
{
    Return x + y;
}
```

```
Static double plusmethoddouble(double x, double y)
{
    Return x + y;
}
```

```
Static void Main(string[] args)
{
    Int mynum1 = plusmethodint(8, 5);
    Double mynum2 = plusmethoddouble(4.3, 6.26);
    Console.writeline("Int: " + mynum1);
```