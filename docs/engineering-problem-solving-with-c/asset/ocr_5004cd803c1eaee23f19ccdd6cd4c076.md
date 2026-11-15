we compute and print a velocity value and increment the time value by 1. When the time value is greater than 10, we exit the chart.

# Pseudocode and Flowchart Description

Algorithms using repetition structures can be described with pseudocode or flowcharts. Figure 4.1 contains the flowchart for a repetition structure that will compute and print a velocity value as long as the time value is less than or equal to 10. The time value is incremented by 1 at the end of each repetition. The pseudocode for this structure is given below:

```
set time to 0
while time <= 10
    compute velocity
    print velocity
    increment time by 1
```

![](bbox=[0.22, 0.355, 0.55, 0.705])

Figure 4.1 Flowchart for repetition structure.

Loops are used to implement repetition structures. C++ contains three different loop structures: the while loop, the do/while loop, and the for loop. C++ also supports the use of two additional statements with loops to modify their performance: the break statement (which we used with the switch statement) and the continue statement. In the remaining sections of this chapter, we present these loop structures and develop example programs that illustrate the use of each of these repetition structures.

# 4.2 Repetition Structures

The most general looping structure in C++ is the while loop.