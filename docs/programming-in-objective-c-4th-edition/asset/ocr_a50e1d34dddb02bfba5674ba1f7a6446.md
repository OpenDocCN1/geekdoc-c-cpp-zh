```
statement
myRect.width = 12;
```

to invoke the Rectangle object's setter method (called initWith: passing it the argument value of 12. No confusion arises here: The compiler determines whether it's a structure or an object to the left of the dot operator and handles the situation properly.

Returning to the struct date example, to set year in today to 2011, you can use this expression:

```
today.year = 2011;
```

Finally, to test the value of month to see whether it is equal to 12, you can use a statement such as this:

```
if ( today.month == 12 )
next_month = 1;
```

Program 13.10 incorporates the preceding discussions into an actual program.

# Program 13.10

```
#import <Foundation/Foundation.h>

int main (int argc, char * argv[]) {
    @autoreleasepool {
        struct date {
            int month;
            int day;
        }
```