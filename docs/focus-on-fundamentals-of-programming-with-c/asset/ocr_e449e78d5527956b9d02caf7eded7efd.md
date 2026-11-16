We now implement our getTomorrowsDate() function as follows:

```
void getTomorrowsDate(Date today, Date *tomorrow) {
    int daysPerMonth[] = {31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30,
31};
    *tomorrow = today;
    tomorrow->day++;
    if (tomorrow->day > daysPerMonth[tomorrow->month-1]) {
        tomorrow->day = 1;
        ++tomorrow->month;
        if (tomorrow->month > 12) {
            tomorrow->month = 1;
            ++tomorrow->year;
        }
    }
}
```

Note that we pass to the function today by value and we pass tomorrow by reference. Why? We do not wish to modify the contents of today but we do want to update the contents of tomorrow. Look how closely our code follows the algorithm we previously developed.

We have one final issue to deal with. What about leap years? We can use the leap year function we previously developed:

```
int isLeapYear(int year) {
    return (((year % 4) == 0 && (year % 100) != 0) || (year % 400));
}
```

Note how we work the test for leap year into the function:

```
int daysPerMonth[] = {31, 0, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31};
if (isLeapYear(today.year)) {
    daysPerMonth[1] = 29;
}
else {
    daysPerMonth[1] = 28;
}
```