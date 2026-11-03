day = (y + j + f - h + fh) % 7;
j = julian day of the date
y = year of given date(in 4 digits)
f = int part of (y-1)/4
h = int part of (y-1)/100
fh = int part of (y-1)/400
The value of variable day tells us the day of week.

| Value of variable day | Name of day of week |
|---|---|
| 0 | Saturday |
| 1 | Sunday |
| 2 | Monday |
| 3 | Tuesday |
| 4 | Wednesday |
| 5 | Thursday |
| 6 | Friday |

In the above formula, julian day of a date represents the day of year on which the date falls. Julian day of 1st Jan is 1, of 2nd Feb is 33, of 31st Dec is 365(366 if leap year).

Now let's decide the structure of our program. Once we get the value of variable day, we can use switch to print the name of day of the week from the value of day.

To calculate the value of day we'll have to find out the value of julian day. Let's assume that the day, month and year of entered date are stored in variables d, m and y respectively. We take another variable j for the value of julian day.

Initially the value of j is taken equal to d, and then days of previous months are added to j to get the value of julian day. We can use switch statement for this and take m as the switch variable.

```
j=d;
switch(m)
{
    case 2:  j+=31;  break;
    case 3:  j+=31+28;  break;
    case 4:  j+=31+28+31;  break;
    case 5:  j+=31+28+31+30;  break;
    case 6:  j+=31+28+31+30+31;  break;
    case 7:  j+=31+28+31+30+31+30;  break;
    case 8:  j+=31+28+31+30+31+30+31;  break;
    case 9:  j+=31+28+31+30+31+30+31+31;  break;
    case 10: j+=31+28+31+30+31+30+31+31+30;  break;
    case 11: j+=31+28+31+30+31+30+31+31+30+31;  break;
    case 12: j+=31+28+31+30+31+30+31+31+30+31+30;  break;
}
```

Suppose the date is 2nd May 2002, then d = 2, m = 5, so the control will go in case 5, and julian day will be 2+31+28+31+30 = 122
The above logic applied in switch statement was simple but as we can see the whole switch statement