```
}
else if (leftHandSide.Day > rightHandSide.Day)
{
    result = 1;
}
else
{
    result = 0;
}
return result;
}
```

You should recognize the form of this logic by now.

If leftHandSide.Day < rightHandSide.Day and leftHandSide.Day > rightHandSide.Day both are false, the value in the Day properties in both variables must be the same. The Month values and the Year values must also be identical, respectively, for the program logic to have reached this point. Therefore, the two dates must be the same, so the program sets the value of result to 0.

The final statement returns the value stored in the result variable.

+   13. On the Debug menu, select Start Debugging to rebuild and run the application.

+   14. Select Compare.

The following text appears in the box:

Click here to view code image

```
firstDate == secondDate : True
firstDate != secondDate : False
firstDate < secondDate : False
firstDate <= secondDate : True
firstDate > secondDate : False
firstDate >= secondDate : True
```

These are the correct results for identical dates.

+   15. Select the DatePicker control to select a later date for the second date (select the tick at the bottom of the control to confirm the selection). Then select Compare.