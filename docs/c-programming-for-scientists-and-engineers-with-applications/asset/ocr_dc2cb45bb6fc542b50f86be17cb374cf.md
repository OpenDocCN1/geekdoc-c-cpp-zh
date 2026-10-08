# 218 Control Structures

![](bbox=[0.315, 0.105, 0.715, 0.513])

Figure 4.8 Flowchart of a for loop

# 4.3.1 Iterative Loops

Iterative loops, also called counting loops, use the keyword for in in C. These loop loop control structures are used to control processing of a known number of data values, to assign index numbers to data or output, or to generate a set of equally spaced numbers.

The flowchart shown in Figure 4.8 might control the numbering of five lines or five pages of output. Or it might control the processing of five data values.

In C, the initialization of the count is retested, the testing of the count, and the increment of the count before it is retested, are all part of the loop header. The C form of this for loop is

```
for(i = 1; i < 6; i++)
```

for is the keyword and i is the loop control variable. The first item specified inside the parentheses i = 1 initializes the loop variable i to a value, the second item i < 6 is a relational expression to control the execution of the loop, as long