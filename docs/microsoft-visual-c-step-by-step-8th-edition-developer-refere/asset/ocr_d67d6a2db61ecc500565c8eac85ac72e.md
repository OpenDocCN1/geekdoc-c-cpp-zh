```
public static string monthName(int month)
{
    switch (month)
    {
        case 1 :
            return "January";
        case 2 :
            return "February";
        ...
        case 12 :
            return "December";

        default :
            throw new ArgumentOutOfRangeException("Bad month");
    }
}
```