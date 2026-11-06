```
```cpp
return testDay == days[month];
}
}

// function to help increment the date
void Date::helpIncrement() {
    // day is not end of month
    if (!endOfMonth(day) {
        ++day; // increment day
    }
    else {
        if (month < 12) { // day is end of month and month < 12
            ++month; // increment month
            day = 1; // first day of new month
        }
        else { // last day of year
            ++year; // increment year
            month = 1; // first month of new year
            day = 1; // first day of new month
        }
    }
}

// overloaded output operator
ostream& operator<<(ostream& output, const Date& d) {
    static string monthName[13]{"", "January", "February",
        "March", "April", "May", "June", "July", "August",
        "September", "October", "November", "December"};
    output << monthName[d.month] << " " << d.day << ", " << d.year;
    return output; // enables cascading
}
```
```

**Fig. 10.7** `Date` class member- and `friend`-function definitions.