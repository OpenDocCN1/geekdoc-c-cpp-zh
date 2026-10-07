# Structures 267

Finally, to test the value of month to see whether it is equal to 12, you can use a statement such as this:

```
if ( today.month == 12 )
next_month = 1;
```

Program 13.10 incorporates the preceding discussions into an actual program.

# Program 13.10

```
#import <Foundation/Foundation.h>
int main (int argc, char *argv[]) {
    NSAutleasePool * pool = [[NSAutleasePool alloc] init];

    struct {
        int month;
        int day;
        int year;
    };

    struct date today;
    today.month = 9;
    today.day = 25;
    today.year = 2011;

    NSLog("%@Today's date is %1i/%1i/%2i.", today.day, today.year, today.year % 100);

    [pool drain]
    return 0;
}
```

# Program 13.10 Output

Today's date is 9/25/11.

The first statement inside defines the structure date to consist of three integers, called month, day, and year. In the second statement, the variable today is declared to be of type date So the first statement simply defines what a date looks like the Objective-C compiler and no storage to be reserved inside the computer. The second statement declares a variable to be of type struct date and, therefore, reserve memory for storing the three integer members of the structure variable today.

After the assignments, appropriate NSLog displays the values contained inside the structure. The remainder of today.year divided by 100 is calculated before passed to the NSLog function that just 1 displays for the year. The %.2i format characters in the NSLog call a minimum of two characters to be displayed, forcing the display of the leading zero for the year.