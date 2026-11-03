```
```c
25    // termination phase
26    average = total / 10; // integer division
27
28    printf( "Class average is %d\n", average ); // display result
29 } // end function main
```
```

```
```
Enter grade: 98
Enter grade: 76
Enter grade: 71
Enter grade: 87
Enter grade: 83
Enter grade: 90
Enter grade: 57
Enter grade: 79
Enter grade: 82
Enter grade: 94
Class average is 81
```
```

**Fig. 3.6** | Class-average problem with counter-controlled iteration. (Part 2 of 2.)

The algorithm mentions a total and a counter. A total is a variable used to accumulate the sum of a series of values. A counter is a variable (line 8) used to count—in this case, to count the number of grades entered. Because the counter variable is used to count from 1 to 10 in this program (all positive values), we declared the variable as an unsigned int, which can store only non-negative values (that is, 0 and higher). Variables used to store totals should be initialized to zero *before* being used in a program; otherwise the sum would include the previous value stored in the total's memory location. Counter variables are normally initialized to zero or one, depending on their use (we'll present examples of each). An uninitialized variable contains a "garbage" value—the value last stored in the memory location reserved for that variable.

> > **Common Programming Error 3.4**
> > If a counter or total isn't initialized, the results of your program will probably be incorrect. This is an example of a logic error.

> > **Error-Prevention Tip 3.4**
> > Initialize all counters and totals.

The averaging calculation in the program produced an integer result of 81. Actually, the sum of the grades in this example is 817, which when divided by 10 should yield 81.7, i.e., a number with a decimal point. We'll see how to deal with such numbers (called floating-point numbers) in the next section.

# **Important Note About the Placement of Variable Definitions**

In Chapter 2, we mentioned that the C standard allows you to place each variable definition anywhere in main before that variable's first use in the code. In this chapter, we continue to group our variable definitions at the beginning of main to emphasize the initialization, processing and termination phases of simple programs. Beginning in Chapter 4, we'll place each variable definition just before that variable's first use. We'll see