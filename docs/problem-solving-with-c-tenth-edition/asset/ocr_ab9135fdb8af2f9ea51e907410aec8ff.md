# DISPLAY 10.4 Class with Private Members (part 2 of 2)

```
42     cin >> month;
43     cout << "Enter the day of the month: ";
44     cin >> day;
45     checkDate();
46 }
47
48 void DayOfYear::output()
    <The rest of the definition of DayOfYear::output is
     given in Display 10.3.>
49
50 void DayOfYear::set(int newMonth, int newDay)
51 {
52     month = newMonth;
53     day = newDay;
54     checkDate();
55 }
56
57 void DayOfYear::checkDate()
58 {
59     if ((month < 1) || (month > 12) || (day < 1) || (day > 31))
60     {
61         cout << "Illegal date. Aborting program.\n";
62         exit(1);
63     }
64 }
65
66 int DayOfYear::getMonth()
67 {
68     return month;
69 }
70
71 int DayOfYear::getDay()
72 {
73     return day;
74 }
```

Private members may be used in member function definitions (but not elsewhere).

A better definition of the member function input would ask the user to reenter the date if the user enters an incorrect date.

The member function checkDate does not check for all illegal dates, but it would be easy to make the check complete by making it longer. See Self-Test Exercise 14.

The function exit is discussed in Chapter 6. It ends the program.

# Sample Dialogue

```
Enter today's date:
Enter the month as a number: 3
Enter the day of the month: 21
Today's date is month = 3, day = 21
J. S. Bach's birthday is month = 3, day = 21
Happy Birthday Johann Sebastian!
```