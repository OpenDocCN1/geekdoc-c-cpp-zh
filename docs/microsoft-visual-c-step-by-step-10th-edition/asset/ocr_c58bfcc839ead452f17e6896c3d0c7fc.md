```
long CalculateFactorial(string input)
{
  ...
  long factorial (int dataValue)
  {
    if (dataValue == 1)
    {
      return 1;
    } else
    {
      return dataValue * factorial(dataValue - 1);
    }
  }
  ...
}
...
```