
However, to run a program with arguments in Xcode, you must first edit the scheme. Under the Product menu, choose Edit Scheme.... When the sheet appears, select Run Affirmation in the table view on the left. Then select the Arguments tab from the choices at the top of the sheet. Find the list entitled Arguments Passed On Launch and use the + button to add two items: a name and a number.

### Figure 36.1 Adding arguments

![](img/5f9368899ebf8d92fc145f8def1e89f8_268_0.png)

Click OK to dismiss the sheet.

When you run the program, you’ll get a list of the strings in *argv*. The one that surprises most people is *argv*[0]:

```
arg 0 = /Users/aaron/Library/Developer/Xcode/DerivedData/Affirmation-enkfqsagavfsproeggxwvbrmcewn/Build/Products/Debug/Affirmation
arg 1 = Aarón
arg 2 = 4
```

*argv*[0] is the path to the executable file.

### Figure 36.2 argv and argc in Affirmation

![](img/5f9368899ebf8d92fc145f8def1e89f8_269_0.png)

If your program takes arguments, the first thing you should do is make sure that the number of arguments is correct. Edit main.m:

```objective-c
#include <stdio.h>
#include <stdlib.h>  // atoi()

int main (int argc, const char * argv[])
{
    if (argc != 3) {
        fprintf(stderr, "Usage: Affirmation <name> <number>\n");
        return 1;
    }

    int count = atoi(argv[2]);
    for (int j = 0; j < count; j++) {
        printf("%s is cool.\n", argv[1]);
    }

    return 0;
}
```

**atoi()** is a standard C function that reads a C string and tries to make an int out of it. Build and run the program.

*This page intentionally left blank*

# 37 Switch Statements

It is not uncommon to check a variable for a set of values. Using *if*-*else* statements, it would look like this:

```
int yeastType = . . . ;

if (yeastType == 1) {
	makeBread();
} else if (yeastType == 2) {
	makeBeer();
} else if (yeastType == 3) {
	makeWine();
} else {
	makeFuel();
}
```

To make this sort of thing easier, C has the *switch* statement. The code above could be changed to this:

```
int yeastType = . . . ;

switch (yeastType) {
	case 1:
		makeBread();
		break;
	case 2:
		makeBeer();
		break;
	case 3:
		makeWine();
		break;
	default:
		makeFuel();
		break;
}
```

Notice the *break* statements. Without the *break*, after executing appropriate case clause, the system would execute all the subsequent case clauses. For example, if I had this:

```
int yeastType = 2;

switch (yeastType) {
	case 1:
	case 2:
		makeBeer();
	case 3:
		makeWine();
	default:
		makeFuel();
}
```

The program would run `makeBeer()`, `makeWine()`, and `makeFuel()`. This is primarily so that you can have multiple possible values trigger the same code:

```
int yeastType = ...;

switch (yeastType) {
    case 1:
    case 4:
        makeBread();
        break;
    case 2:
    case 5:
        makeBeer();
        break;
    case 3:
        makeWine();
        break;
    default:
        makeFuel();
        break;
}
```

As you can imagine, forgetting to put the break at the end of the case clause is a common programmer error, and it is only discovered when your program starts acting strangely.

In C, switch statements are for a very specific situation: the case can only be a constant integer. As such, you don’t see a lot of switch statements in most Objective-C programs. Which is why I snuck it in here just before the book ends.

# Next Steps

Well, that’s everything you will ever need to know to write brilliant applications for iOS and Mac OS X.

That’s what I wish I could tell you. I know you’ve worked hard to get to this point.

The truth is that you have completed the first leg of a fun and rewarding journey. It is, however, a very long journey. It is now time for you to spend some time studying the standard frameworks that Apple makes available to Objective-C developers like you.

Let me repeat that last phrase so you can relish it: “Objective-C developers like you.” Congratulations.

If you are learning to develop applications for iOS, I recommend that you work through *iOS Programming: The Big Nerd Ranch Guide*, but there are several other books on iOS, and you are ready for any of them.

If you are learning to develop applications for Mac OS X, I recommend that you work through *Cocoa Programming for Mac OS X*, but, here again, there are several other books on Cocoa, and you are ready for any of them.

There are groups of developers who meet every month to discuss the craft. In most major cities, there are iOS Developers Meetups and CocoaHeads chapters. The talks are often surprisingly good. There are also discussion groups online. Take some time to find and use these resources.

# Shameless plugs

You can find me on Twitter, where I post news about Big Nerd Ranch: @AaronHillegass

Keep an eye out for future guides from Big Nerd Ranch. We also offer week-long courses for developers. And if you just need some code written, we do contract programming. For more information, visit our website at www.bignerdranch.com.

It is you, dear reader, who makes my life of writing, coding, and teaching possible. So thank you for buying my book.

*This page intentionally left blank*

# Index

! (logical NOT) operator, 24  
!= (not equal) operator, 23  
\ escape sequence, 248  
\#define, 145-147  
\#import, 146  
\#include, 146  
% (modulus operator), 44  
(see also tokens)  
%= operator, 46  
%@, 119  
%d, 41  
%E, 46  
%p, 56  
%s, 41  
%u, 43  
%zu, 58  
& operator, retrieving addresses, 55  
&& (logical AND) operator, 24  
() (parentheses)  
- cast operators, using, 45  
- functions and, 28, 31  
* (asterisk)  
- arithmetic operator, 44  
- pointer operator, 57  
*= operator, 46  
+ (plus sign), 44  
++ (increment operator), 45  
+= operator, 46  
- (minus sign), 44  
-- (decrement operator), 45  
-= operator, 46  
-> (dereference) operator, 71  
.pch (pre-compiled header), 146  
/ (division operator), 44  
/\* … \*/ (comments), 12  
// (comments), 12  
/= operator, 46  
8-bit unsigned numbers, 42  
; (semicolon), 12  
blocks and, 230  
do-while loop and, 54  
< (less than) operator, 23  

A  
abs(), 46  
- accessor methods, 103-105  
- properties and, 217  
actions (target), 157  
addObject::, 135  
addresses, 55-59  
- pointers and, 20  
alloc, 81, 207  
ampersand (&), retrieving addresses, 55  
AND (&&) logical operator, 24  
AND (bitwise), 241  
angle brackets (< >), importing header files, 146  
anonymous  
- blocks, 235  
- functions, 227  
Apple Developer Tools, installing, 7  
application:didFinishLaunchingWithOptions:, 183-190  
applications  
- (see also programs, Xcode)  
- Cocoa, 191-204  
- Cocoa Touch, 177-190  
- desktop, 191-204  
- document-based, 192  
< > (angle brackets), importing header files, 146  
<< operator, 244  
<= operator, 23  
= operator, 22, 24  
== operator, 23, 24  
> (greater than) operator, 23  
>= operator, 23  
>> operator, 244  
? (ternary operator), 26  
@property, 105  
@selector(), 159  
@synthesize, 105  
\\ (backslash), 248  
\n, 41  
\\ escape sequence, 248  
^ (caret)  
- exclusive-or operator, 243  
- identifying blocks, 227  
{} (curly braces), 12  
|| (logical OR) operator, 24  
~ (tilde), 243

+ event-driven, 175  
- iOS, 177-190  
- vs. programs, 7  
- ARC (Automatic Reference Counting), 117-123  
- arguments  
  - command-line, 257-259  
  - functions, 28  
  - init, 210  
  - methods, 82  
- arrays, 87-89  
  - in C, 253-255  
  - filtering, 137  
  - sorting, 136  
- ASCII characters, 151, 247  
- assembly code, 3  
- asterisk (*)  
  - arithmetic operator, 44  
  - pointer operator, 57  
- AT&T, 4  
- atoi(), 259  
- atomic option, 220  
- attributes inspector, 194  
- Automatic Reference Counting (ARC), 117-123  
- automatic variables, 69  
- autosizing mask, 196  

**B**  
- backslash (\\), 248  
- base-16 (hexadecimal)  
  - integers, 43  
  - number system, 239  
- base-8 (octal) integers, 43  
- bits, 55  
- bitwise AND, 241  
- bitwise operations, 239-245  
- bitwise OR, 240  
- __block keyword, 235  
- blocking (functions), 31  
- blocks, 227-236  
  - anonymous, 235  
  - defining, 227  
  - return values of, 233  
  - variables, 228  
- BOOL (type), 25  
- boolean variables, 24  
- break statement, 51  
- breakpoint navigator, 37  
- breakpoints, 36  
- buffers, 69  
- bugs, 35  
- building programs, 13  
- bytes, 55, 239  

**C**  
- C programming language, 3, 4  
  - arrays, 253-255  
  - primitive types, 142  
  - strings, 247-252  
- callbacks, 157-164, 227  
  - memory management and, 164, 165  
- calling functions, 28  
- captured variables, 234  
- caret (^)  
  - exclusive-or operator, 243  
  - identifying blocks, 227  
- cast operator, 45  
- Central Processing Unit (CPU), 55  
- char (type), 20, 247  
  - as 8-bit number, 42  
- char * (type), 41  
- class methods, 81  
- class prefixes, 179  
- classes, 75, 101-106  
  - (see also objects, *individual class names*)  
- closures, 227  
- Cocoa, 175, 191-204  
- Cocoa Touch, 175  
- code completion, 12  
- collection classes, 135-143  
  - (see also arrays)  
- command-line arguments, 257-259  
- command-line tools  
  - in C, 8  
  - defined, 8  
  - Foundation, 75  
- compilers, 3, 15  
- complements, 243  
- conditional expressions, 23-26  
- constants, 145-149  
- continue statement, 52  
- controller objects (MVC), 182  
- controls, 189  
- convenience methods, 134  
- copy (method), 219, 220
