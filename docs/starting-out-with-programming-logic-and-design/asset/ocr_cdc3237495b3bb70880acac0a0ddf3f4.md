# 7.2 The Input Validation Loop 273

```
3 Declare String doAnother
4 Do
5 // Calculate and display a retail price.
6 Call showRetail()
7
89 // Do this again?
10 Display "Do you have another item? (Enter y for yes.)"
11 Input doAnother
12 While doAnother = "y" OR doAnother = "y"
13 End Module
14
15 // The ShowRetail module gets an item's wholesale cost
16 // from the user and displays its retail price.
17 module showRetail()
18 // Local variables
19 Declare Real wholesale, retail
20
21 // Constant for the markup percentage
22 Declare Real MARKUP = 2.50
23
24 // Get the wholesale cost.
25 Display "Enter an item's wholesale cost."
26 Input wholesale
27
28 // Validate the wholesale cost.
29 While wholesale < 0
30 Display "The cost cannot be negative. Please"
31 Display "enter the correct wholesale cost."
32 Input wholesale
33 End While
34
35 // Calculate the retail price.
36 Set retail = wholesale * MARKUP
37
38 // Display the retail price.
39 Display "The retail price is $\$, retail
40 End Module
```

# Program Output (with Input Shown in Bold)

Enter an item's wholesale cost.
**-0.50 [Enter]**nThe cost cannot be negative. Please enter the correct wholesale cost.
**0.50 [Enter]**
The retail price is $1.25
Do you have another item? (Enter y for yes.)
**n [Enter]**