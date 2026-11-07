# **Program 2.3** A program that adds two values (Continued)

```
~~~cpp
16    cin >> num1;
17    cout << "Enter the second number: ";
18    cin >> num2;
19    // Calculation and storing result
20    sum = num1 + num2;
21    // Display output
22    cout << "The sum is: " << sum;
23    return 0;
24 }
~~~
```

```
~~~
Run:
Enter the first number: 23
Enter the second number: 35
The sum is: 58

Run:
Enter the first number: 7
Enter the second number: 110
The sum is: 117
~~~
```

We examine the contents of lines 11 to 13 as shown below:

```
~~~cpp
int num1;
int num2;
int sum;
~~~
```

These three lines declare variables. Declaration of a variable means reservation of memory with a corresponding name. In the case of the above three declarations, we have the situation shown previously in Figure 2.5. Note that no values are stored in the program at this moment.

Now we examine lines 15 to 18 as shown below:

```
~~~cpp
cout << "Enter the first number: ";
cin >> num1;
cout << "Enter the second number: ";
cin >> num2;
~~~
```

We are familiar with the first line. The first line prints a message, which is referred to as *prompt*, on the screen. It tells the user what to do next. The second line is new for us. It uses a target object, `cin` (for console in) and a command (`>>`), which means *read*. This command waits for the user of the program to enter a value (an integer in this case) on the keyboard and hit the enter key. The program then stores the value entered in variable `num1`. The third line is the same as the first one. The fourth line is the same as the second line, but it stores the value entered by the user in variable `num2`. After these four lines, two values are stored