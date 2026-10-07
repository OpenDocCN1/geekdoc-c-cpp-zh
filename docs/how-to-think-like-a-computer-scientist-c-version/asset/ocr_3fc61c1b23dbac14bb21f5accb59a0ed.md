# 9.4. PURE FUNCTIONS

```
if (time1.minute > time2.minute) return true;
if (time1.minute < time2.minute) return false;
```

```
if (time1.second > time2.second) return true;
return false;
}
```

What is the result of this function if the two times are equal? Does that seem like the appropriate result for this function? If you were writing the documentation for this function, would you mention that case specifically?
A second example is addTime, which calculates the sum of two times. For if it is 9:14:30, and your breadmaker takes 3 hours and 35 minutes, you could use addTime to figure out when the bread will be done.
Here is a rough draft of this function that is not quite right:

```
addTime(Time t1, Time t2) {
sum = ;
sum.hour = t1.hour + t2.hour;
sum.minute = t1.minute + t2.minute;
sum.second = t1.second + t2.second;
return sum;
}
```

Here is an example of how to use this function. If currentTime contains the current time and breadTime contains the amount of it takes for your breadmaker, then you could use addTime to figure out when the bread will be done.

```
Time currentTime = { 9, 14, 30.0 };
Time breadTime = { 3, 35, 0.0 };
Time doneTime = addTime(currentTime, breadTime);
printTime(doneTime);
```

The output of this program is 12:49:30, which is correct. On the other hand, there are cases where the result is not correct. Can you think of one?
The problem is that this function does not deal with cases where the number of seconds or minutes adds up more than 60. When that happens we have to "carry" the extra seconds into the minutes column, or extra minutes into the hours column.
Here's a second, corrected version of this function.

```
addTime(Time t1, Time t2) {
sum = ;
sum.hour = t1.hour + t2.hour;
sum.minute = t1.minute + t2.minute;
sum.second = t1.second + t2.second;
```