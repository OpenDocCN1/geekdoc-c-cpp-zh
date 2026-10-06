The getCups module has a parameter, cups, which is a reference variable. The module prompts the user to enter the number of cups and stores the user's input in the cups parameter. When the main module calls getCups, it will pass the local variable as an argument. Because it is passed by reference, it will contain the user's input when the module returns. Program 3-11 shows the revised pseudocode for the program, and Figure 3-19 shows a flowchart.

> NOTE: In this case study, we improved the design of an existing program without changing the behavior of the program. In a nutshell, we "cleaned up" the design. Programmers call this refactoring.

# Program 3-11

```
1 Module main()
2 // Declare a variable for
3 // number of cups needed.
4 Declare Real cupsNeeded
5
6 // Display an intro message.
7 Call showIntro()
8
9\10 // Get the number of cups.
11 Call getCups(cupsNeeded)
12
13 // Convert cups to ounces.
14 Call cupsToOunces(cupsNeeded)
15 End Module
16
17 // The showIntro module displays an
18 // introductory screen.
19 Module showIntro()
20 Display "This program converts measurements"
21 Display "  in cups to fluid ounces. For your"
22 Display "    reference the formula is:"
23 Display "    1 cup = 8 fluid ounces."
24 End Module
25
26 // The getCups module gets the number of cups
27 // and stores it in the reference variable cups.
28 Module getCups(Real Ref cups)
29 Display "Enter the number of cups."
30 Input cups
31 End Module
32
33 // The cupsTounces module accepts a number
34 // of cups and displays the equivalent number
35 // of ounces.
36 Module cupsToOunces(Real cups)
37 // Declare variables.
38 Declare Real ounces
39
40 // Convert cups to ounces.
```