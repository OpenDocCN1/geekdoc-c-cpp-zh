# Step 6—Evaluate and Modify the Program

(continued)

```
11 double liquor = 0.0;
12 double tipPercent = 0.0;
13 double totalNoLiquor = 0.0;
14 double tip = 0.0;
15
16 //enter input items
17 cout << "Enter the total bill: ";
18 cin >> totalBill;
19 cout << "Enter the liquor charge: ";
20 cin >> liquor;
21 cout << "Enter the tip percentage in decimal format: ";
22 cin >> tipPercent;
23
24 //calculate the total without liquor and the tip
25 totalNoLiquor = totalBill - liquor;
26 tip = totalNoLiquor * tipPercent;
27
28 //display the output item
29 cout << "Tip: $$" << tip << endl;
30 system("pause");
31 return 0;
33 } //end of main function
```

![](bbox=[0.927, 0.183, 0.982, 0.203])

> depending on your C++ developpement tool, this statement may not be necessary

Figure-20 Treyson model program

Lines 1, 2, 9, 16, 24 and 28 in the program; there is also a comment on line 33. You create a comment by typing forward slashes (//) before the text you treated as a comment. A comment is simple to use a message to the person reading the program and is referred to as documentation. The comments on lines 1 and 2 identify the program's name and purpose, as well as the programmer's name and the date the program was either created or revised. The remaining comments explain various sections of the code. The C++ compiler indicates that they follow are variable declarations does not require you to include comments in a program. However, it is good programming practice to do so because they make your code more readable and easier to understand by anyone viewing it. The C++ compiler does not process (execute) the comments in a program. Instead, the compiler ignores the comments when it translates the source code into object code. Comments do not end with a semicolon, they are not statements in C++.

Lines 4 and 5 in Figure 4-20 are directives; line 4 is #include directive and line 5 is a directive. The #include directive provides a convenient way to merge the source code from one file with another file, without having to retype the code. The #Include <iostream> directive, for example, tells the C++ compiler to include the contents of the istream in the current program. The istream must be included in any program that uses the cin or cout objects. A #include directive is not a C++ statement; therefore, it does not end with a semicolon. A using directive, on the other hand, is a statement; therefore, it must end with a semicolon. A using directive tells the compiler (in the computer's internal memory) it find the definitions