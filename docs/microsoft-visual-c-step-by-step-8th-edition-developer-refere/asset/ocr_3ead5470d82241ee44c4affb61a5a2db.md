```
} // myVar disappears here
else
{
    // myVar cannot be used here
    ...
}
// myVar cannot be used here
```

# Cascading if statements

You can nest if statements inside other if statements. In this way, you can chain together a sequence of Boolean expressions, which are tested one after the other until one of them evaluates to true. In the following example, if the value of day is 0, the first test evaluates to true and dayName is assigned the string “Sunday”. If the value of day is not 0, the first test fails and control passes to the else clause, which runs the second if statement and compares the value of day with 1. The second if statement executes only if the first test is false. Similarly, the third if statement executes only if the first and second tests are false.

```
if (day == 0)
{
    dayName = "Sunday";
}
else if (day == 1)
{
    dayName = "Monday";
}
else if (day == 2)
{
    dayName = "Tuesday";
}
else if (day == 3)
{
    dayName = "Wednesday";
}
else if (day == 4)
{
    dayName = "Thursday";
}
else if (day == 5)
{
    dayName = "Friday";
}
else if (day == 6)
{
    dayName = "Saturday";
}
else
{
    dayName = "unknown";
}
```

In the following exercise, you’ll write a method that uses a cascading if statement to compare two dates.