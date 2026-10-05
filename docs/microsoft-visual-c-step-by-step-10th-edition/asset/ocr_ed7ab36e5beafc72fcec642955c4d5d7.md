```
private int dateCompare(DateTime leftHandSide, DateTime rightHandSide)
{
    int result = 0;
    if (leftHandSide.Year < rightHandSide.Year)
    {
        result = -1;
    }
    else if (leftHandSide.Year > rightHandSide.Year)
    {
        result = 1;
    }
}
```