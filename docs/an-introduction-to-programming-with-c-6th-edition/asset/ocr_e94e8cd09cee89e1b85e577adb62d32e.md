# Answers to TRY THIS Exercises

# Pencil and Paper

+   1. See Figure 6-49.

```
if (monthNum == 1)
    cout << "January";
else if (monthNum == 2)
    cout << "February";
else if (monthNum == 3)
    cout << "March";
else if (monthNum == 4)
    cout << "April";
else if (monthNum == 5)
    cout << "May";
else if (monthNum == 6)
    cout << "June";
else if (monthNum == 7)
    cout << "July";
else if (monthNum == 8)
    cout << "August";
else if (monthNum == 9)
    cout << "September";
else if (monthNum == 10)
    cout << "October";
else if (monthNum == 11)
    cout << "November";
else if (monthNum == 12)
    cout << "December";
else
    cout << "Incorrect month number";
//end if
```

Figure 6-49

+   2. See Figure 6-50.

```
switch (code)
{
    case '1':
        rate = .02;
        break;
    case '2':
    case '3':
    case '4':
        rate = .05;
        break;
    case '5':
        rate = .1;
        break;
    case '6':
    case '7':
        rate = .15;
        break;
    default:
        rate = -1;
} //end switch
```

Figure 6-50