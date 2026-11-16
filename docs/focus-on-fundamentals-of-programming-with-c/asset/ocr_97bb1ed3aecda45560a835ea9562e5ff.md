# Our complete program looks like this:

```
```c
#include <stdio.h>

typedef struct {
    int month;
    int day;
    int year;
} Date;

void getTodaysDate(Date *today);
void getTomorrowsDate(Date today, Date *tomorrow);
int isLeapYear(int year);
void outputDate(Date d);

int main(void) {
    Date today, tomorrow;

    getTodaysDate(&today);
    getTomorrowsDate(today, &tomorrow);

    printf("Today: ");
    outputDate(today);
    printf("Tomorrow: ");
    outputDate(tomorrow);

    return 0;
}

void getTodaysDate(Date *today) {
    printf("Enter today's date mm/dd/yyyy: ");
    scanf("%d/%d/%d", &today->month, &today->day, &today->year);
}

void getTomorrowsDate(Date today, Date *tomorrow) {
    int daysPerMonth[] = { 31, 0, 31, 30, 31, 30, 31, 31,
                           30, 31, 30, 31 };

    if (isLeapYear(today.year)) {
        daysPerMonth[1] = 29;
    }
    else {
        daysPerMonth[1] = 28;
    }

    *tomorrow = today;
    tomorrow->day++;
}
```
```