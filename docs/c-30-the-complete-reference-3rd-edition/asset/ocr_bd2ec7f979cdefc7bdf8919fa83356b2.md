```
```csharp
// Use continue.
using System;

class ContDemo {
    static void Main() {
        // Print even numbers between 0 and 100.
        for(int i = 0; i <= 100; i++) {
            if((i%2) != 0) continue; // iterate
            Console.WriteLine(i);
        }
    }
}
```
```

Only even numbers are printed, because an odd number will cause the loop to iterate early, bypassing the call to WriteLine().

In while and do-while loops, a continue statement will cause control to go directly to the conditional expression and then continue the looping process. In the case of the for, the iteration expression of the loop is evaluated, then the conditional expression is executed, and then the loop continues.

Good uses of continue are rare. One reason is that C# provides a rich set of loop statements that fit most applications. However, for those special circumstances in which early iteration is needed, the continue statement provides a structured way to accomplish it.

# return

The return statement causes a method to return. It can also be used to return a value. It is examined in Chapter 6.

# The goto

The goto is C#'s unconditional jump statement. When encountered, program flow jumps to the location specified by the goto. The statement fell out of favor with programmers many years ago because it encouraged the creation of "spaghetti code." However, the goto is still occasionally—and sometimes effectively—used. This book will not make a judgment regarding its validity as a form of program control. It should be stated, however, that there are no programming situations that require the use of the goto statement—it is not necessary for making the language complete. Rather, goto is a convenience that, if used wisely, can be a benefit in certain programming situations. As such, the goto is not used in this book outside of this section. The chief concern most programmers have about the goto is its tendency to clutter a program and render it nearly unreadable. However, there are times when the use of the goto can clarify program flow rather than confuse it.

The goto requires a label for operation. A label is a valid C# identifier followed by a colon. The label must be in the same method as the goto that uses it and within scope. For example, a loop from 1 to 100 could be written using a goto and a label, as shown here:

```
```csharp
x = 1;
loop1:
x++;
if(x < 100) goto loop1;
```
```