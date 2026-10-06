
The primary change made to the NSLog statement is the inclusion of a field width specification. The characters %2i tell the NSLog routine not only that you want to display the value of an integer at that particular point, but also that the size of the integer to be displayed should take up at least two columns in the display. Any integer that would normally take less than two columns (that is, the integers 0-9) will be displayed with a leading space. This is known as right justification.

Thus, by using a field width specification of %2i, you guarantee that at least two columns will be used for displaying the value of n; you also ensure that the values of triangularNumber will be aligned.

## Keyboard Input

Program 5.2 calculates the 200th triangular number, and nothing more. What if you wanted to calculate the 50th or the 100th triangular number instead? Well, if that were the case, you would have to change the program so that the for loop would be executed the correct number of times. You would also have to change the NSLog statement to display the correct message.

An easier solution might be to somehow have the program ask you triangular number you want to calculate. Then, after you had given your answer, the program could calculate the desired triangular number. You can effect such a solution by using a routine called scanf. The scanf routine is similar in concept to the NSLog routine. Whereas the NSLog routine is used to display values, the purpose of the scanf routine is to enable the programmer to type values into the program. Of course, if you're writing an Objective-C program that uses a graphical User Interface (UI), such as a Cocoa or iOS application, you likely won't be using NSLog or scanf at all in your program.

Program 5.4 asks the user which triangular number should be calculated, calculates that number, and then displays the results.

## Program 5.4

```
#import <Foundation/Foundation.h>

int main (int argc, char * argv[]) {
    @autoreleasepool {
        int n, number, triangularNumber;

        NSLog ("@What triangular number do you want?");
        scanf("%i", &number);

        triangularNumber = 0;

        for ( n = 1; n <= number; ++n) {
            triangularNumber += n;
        }

        NSLog ("@Triangular number %i is %i\n", number, triangularNumber);
    }

    return 0;
}
```

In the program output follows, the number typed by the user **(100)** is set in bold type, to distinguish it from the output displayed by the program.

## Program 5.4. Output

# # What triangular number do you want?
100
Triangular number 100 is 5050

According to the output, the user typed the number 100. The program then calculated the 100th triangular number and displayed the result of 5050 at the terminal. The user could have easily typed in the number 10 or 30, for example, if he or she wanted to calculate those particular triangular numbers.

The first NSLog statement in Program 5.4 is used to prompt the user to type in a name. Of course, it is always nice to remind the user of what you want entered. After the message is printed, the scanf routine first argument is the format string, which does not begin with the @ character. Unlike NSLog, first argument is an NSString object, the first argument to scanf is a C-style string. As noted earlier in this text, C-style character strings are not preceded by the @ character.

The format string tells scanf what types of values are to be read from the console (or terminal window, if you're compiling your programs using the Terminal application). With NSLog, the %i characters are used to specify an integer value.

The second argument to the scanf routine specifies where the value that the user types is to be stored. The & character before the variable number is necessary in this case. Rather than supplying the value of the variable number, we instead specify where we want the value that is entered to be stored. Don't worry about this right now. We discuss this character, which is actually an operator, in great detail when we talk about pointers in Chapter 13.

Given the preceding discussion, you can now see that the scanf call from Program 5.4 specifies that an integer value is to be read and stored into the variable number. This value represents the particular triangular number the user wants to have calculated.

After the user has typed in this number (and pressed the Enter key on the keyboard to signal that typing of the number is completed), the program calculates the requested triangular number. This is done in the same way as in Program 5.2; the only difference is that, instead of using 200 as the limit, number is used as the limit.

> Note
> Pressing the Enter key on a keyboard with a numeric keypad may not cause the number you enter to be sent to the program. Use the Return key on your keyboard instead.

After the desired triangular number has been calculated, the results are displayed. Execution of the program is then complete.

## Nested for Loops

Program 5.4 gives the user the flexibility to have the program calculate any triangular number that is desired. But suppose the user had a list of five triangular numbers to be calculated? In such a case, the user could simply execute the program five times, each time typing in the next triangular number from the list to be calculated.

Another way to accomplish the same goal, and a far more interesting method, as far as learning about Objective-C is concerned, is to have the program handle the situation. This can be best accomplished by inserting a loop into the program to repeat the entire series of calculations five times. You can use the for statement to set up such loop. Program 5.5 and its associated output illustrate this technique.

## Program 5.5

```
#import <Foundation/Foundation.h>

int main (int argc, char * argv[]) {
    @autoreleasepool {
        int n, number, triangularNumber, counter;

        for ( counter = 1; counter <= 5;
        ++counter ) {
            NSLog (@"What triangular number do you
        want?");
            scanf("%i", &number);

            triangularNumber = 0;

            for ( n = 1; n <= number; ++n ) {
                triangularNumber += n;
                NSLog (@"Triangular number %i is %i",
                number, triangularNumber);
            }
        }
    }

    return 0;
}
```

## Program 5.5. Output

What triangular number do you want?
12
Triangular number 12 is 78

What triangular number do you want?
25
Triangular number 25 is 325

What triangular number do you want?
50
Triangular number 50 is 1275

What triangular number do you want?
75
Triangular number 75 is 2850

What triangular number do you want?
83
Triangular number 83 is 3486

The program consists of two levels of for statements. The outermost for-statement is as follows:

```
for ( counter = 1; counter <= 5; ++counter )
```

This specifies that the program loop is to be executed precisely five times. The value of counter is initially set to 1 and is incremented by 1 until it is no longer less or equal to 5 (in other words, until it reaches 6).

Unlike the previous program examples, the variable counter is not used anywhere else within the program. Its function is solely as a loop counter in the for statement. Nevertheless, because it is a variable, you must declare it in the program.

...

Before leaving this discussion of the for loop, we should mention some of the syntactic variations that are permitted in forming this loop. When writing a for loop, you might discover that you want to initialize more than one variable before the loop begins, or perhaps you want to evaluate more than one expression each time through the loop. You can include multiple expressions in any of the fields of the for loop, as long as you separate expressions by commas. For example, in the for statement begins

```
for ( i = 0, j = 0; i < 10; ++i )
```
