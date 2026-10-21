```
```cpp
Time2.ShowTime();
Time Time3;
Time3 = Difference(Time1, Time2);
/* Call to the function that accepts and returns the object */
cout << "And the difference is \n";
Time3.ShowTime();
}

/* Definition of the function that accepts and returns the object */
Time Difference(Time T1, Time T2)
{
Time DifferenceTime;
DifferenceTime.Seconds = T1.Seconds - T2.Seconds;
if(DifferenceTime.Seconds < 0)
{
DifferenceTime.Seconds += 60;
T1.Minutes--; // Borrowing from minutes
if(T1.Minutes < 0)
{
T1.Minutes = 59;
T1.Hours--; // Borrowing from hours
}
}

DifferenceTime.Minutes = T1.Minutes - T2.Minutes;
if(DifferenceTime.Minutes < 0)
{
DifferenceTime.Minutes += 60;
T1.Hours--; // borrowing from hours
}

DifferenceTime.Hours = T1.Hours - T2.Hours;
if(DifferenceTime.Hours < 0)
{
DifferenceTime.Hours = 0;
DifferenceTime.Minutes = 0;
DifferenceTime.Seconds = 0;
// To indicate erroneous input
}

return DifferenceTime;
}
```
```

```
```
Output

The first value

Time is 12 hours: 15 minutes: and 15 seconds

The second value

Time is 10 hours: 30 minutes: and 30 seconds

And the difference is

Time is 1 hour: 44 minutes: and 45 seconds
```
```

# # How the Program Works

See how the function Difference() is used. Two arguments are passed to it, both of type Time.

It should be observed that there is no difference in the syntax while passing objects or any other data type to the function. When the function call is made, the actual arguments (objects in this case) are copied to the dummy arguments of the function. By default, an exact copy is made from the actual argument objects to the dummy argument objects in this case. This