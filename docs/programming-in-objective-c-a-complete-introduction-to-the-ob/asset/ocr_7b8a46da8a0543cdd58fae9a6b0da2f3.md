```
NSLog("@Sign = %i", sign);
[pool drain];
return 0;
```

# Program 6.6 Output

Please type in a number:
1121
Sign = 1

# Program 6.6 Output (Rerun)

Please type in a number:
-158
Sign = -1

# Program 6.6 Output (Rerun)

Please type in a number:
0
Sign = 0

> If the number that is entered is less than zero, sign is assigned the value -1; if the number is equal to zero, sign is assigned the value 0; otherwise, the number must be greater than zero, sign is assigned the value 1.
The next program analyzes a character that is typed in from the terminal and classifies it as either an alphabetical character (a–z or A–Z), a digit (0–9), or a special character (anything else). To read a single character from the terminal, the format characters %c are used in the scanc file.

# Program 6.7

```
// This program categorizes a single character
// that is entered from the keyboard

#import <Foundation/Foundation.h>
int main (int argc, char *argv[]) {
    NSAutleasePool *pool = [NSAutleasePool alloc init];
    char *c;

    NSLog("@Enter a single character:");
    scancf("%%c", &c);

    if ( c >= 'a' && c <= 'z') || ( c >= 'A' && c <= 'Z') {
        NSLog("@It\'s an alphabetical character.");
    } else if ( c >= '0' && c <= '9') {
        NSLog("@It\'s a digit.");
    }
```