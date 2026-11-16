```
#include <stdio.h>

struct date {
    int month;
    int day;
    int year;
};

void printDate(struct date *pd) {
    printf("%d/%d/%d", pd->month, pd->day, pd->year);
}

void main(void) {
    struct date d = { 9, 18, 2012 };

    printf("Today's date is ");
    printDate(&d);
    printf("\n");
}
```

In C++, the designer of a user-defined type provides an instance of the output operator for the type. Clients of the type need know nothing about how its output is handled. For example:

```
#include <iostream>

using namespace std;

struct date {
    int month;
    int day;
    int year;
};

ostream& operator<<(ostream& os, date &d) {
    os << d.month << "/" << d.day << "/" << d.year;
    return os;
}

int main() {
    struct date d = { 9, 18, 99 };

    cout << "Today's date is " << d << endl;
}
```

Again, there's no need to worry about the syntax for now.