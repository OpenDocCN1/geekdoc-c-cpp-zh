# Chapter 8: Performing Iterative Processing: Looping 115

The block of code between the WHILE and AND statements executes as long as Total is less than or 200. Output from this program is identical to Program 8.13.

To reinforce the idea that WHILE conditions are tested at the top of the loop, look at this program:

# Program 8.16: Demonstrating That WHILE Loops Are Evaluated At The Top

```
data Double;
Interest = .0375;
Total = 300;
do while (Total lt 200)
Year = +1;
Total = Total + Interest*Total;
output;
end;
format Total dollar10.2;
run;
```

Because the WHILE condition is never true, the statements inside the DO block never execute and the data set Double has no observations.

# 8.7 A Caution When Using DO UNTIL Statements

It is very important that the condition you place on a DO UNTIL statement becomes true at some point. For example, if you change the DO UNTIL statement in Program 8.14 to read as follows, the condition is never true and you have what is called an infinite loop:

```
do until (Total eq 200);
```

Depending on whether or not you are paying for your computer time, this could be a bad (expensive) thing. On a PC platform, you can usually interrupt the program by selecting the icon to stop a SAS program (the exclamation point on the taskbar) or simultaneously clicking the CTRL and C keys. The lesson here is to be very careful when using a DO UNTIL statement: make sure the condition you specify eventually returns a true value.

One way to prevent infinite loops is to combine a regular DO loop with an UNTIL condition. Rewrite program like this:

# Program 8.17: Combining a DO UNTIL and Iterative DO Loop

```
data Double;
Interest = .0375;
Total = 100;
do Year = 1 to 100 until (Total gt 200)
Total = Total + Interest*Total;
output;
end;
format Total dollar10.2;
run;
```