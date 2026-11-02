
```
if (cin.fail())
{
    cout << "Error: Not an integer." << endl;
    return 1;
}
if (floor == 13)
{
    cout << "Error: There is no thirteenth floor." << endl;
    return 1;
}
if (floor <= 0 || floor > 20)
{
    cout << "Error: The floor must be between 1 and 20." << endl;
    return 1;
}

// Now we know that the input is valid
int actual_floor;
if (floor > 13)
{
    actual_floor = floor - 1;
}
else
{
    actual_floor = floor;
}

cout << "The elevator will travel to the actual floor "
    << actual_floor << endl;

return 0;
}
```

## Program Run

Floor: 13
Error: There is no thirteenth floor.

![](img/d61019b035dd82beb581604273c0ee6b_147_0.png)

## Computing & Society 3.2 Artificial Intelligence

When one uses a sophisticated computer program such as a tax preparation package, one is bound to attribute some intelligence to the computer. The computer asks sensible questions and makes computations that we find a mental challenge. After all, if doing one's taxes were easy, we wouldn't need a computer to do it for us.

As programmers, however, we know that all this apparent intelligence is an illusion. Human programmers have carefully "coached" the software in all possible scenarios, and it simply replays the actions and decisions that were programmed into it.

Would it be possible to write computer programs that are genuinely intelligent in some sense? From the earliest days of computing, there was a sense that the human brain might be nothing but an immense computer, and that it might well be feasible to program computers to imitate some processes of human thought. Serious research into artificial intelligence began in the mid-1950s, and the first twenty years brought some impressive successes. Programs that play chess—surely an activity that appears to require remarkable intellectual powers—have become so good that they now routinely beat all but the best human players. As far back as 1975, an expert-system program called Mycin gained fame for being better in diagnosing meningitis in patients than the average physician.

From the very outset, one of the stated goals of the AI community was to produce software that could translate text from one language to another, for example from English to Russian. That undertaking proved to be enormously complicated. Human language appears to be much more subtle and interwoven with the human experience than had originally been thought. Systems such as Apple's Siri can answer common questions about the weather, appointments, and traffic. However, beyond a narrow range, they are more entertaining than useful.

In some areas, artificial intelligence technology has seen substantial advances. One of the most astounding examples is the rapid development of self-driving car technology. Starting in 2004, the Defense Advanced Research Projects Agency (DARPA) organized a series of competitions in which computer-controlled vehicles had to complete an obstacle course without a human driver or remote control. The first event was a disappointment, with none of the entrants finishing the route. In 2005, five vehicles completed a grueling 212 km course in the Mojave desert. Stanford's Stanley came in first, with an average speed of 30 km/h. In 2007, DARPA moved the competition to an "urban" environment, an abandoned air force base. Vehicles had to be able to interact with each other, following California traffic laws. Self-driving cars are now tested on public roads in several states, and it is expected that they will become commercially available within a decade. When a system with artificial intelligence replaces a human in an activity such as giving medical advice or driving a vehicle, an important question arises. Who is responsible for mistakes? We accept that human doctors and drivers occasionally make mistakes with lethal consequences.

Will we do the same for medical expert systems and self-driving cars?

![](img/d61019b035dd82beb581604273c0ee6b_148_0.png)

Vaughn Youtz/Zuma Press.

Winner of the 2007 DARPA Urban Challenge

## CHAPTER SUMMARY

### Use the if statement to implement a decision.
- The if statement allows a program to carry out different actions depending on the nature of the data to be processed.

![](img/d61019b035dd82beb581604273c0ee6b_148_1.png)

### Implement comparisons of numbers and objects.
- Relational operators (< <= > >= == !=) are used to compare numbers and strings.
- Lexicographic order is used to compare strings.

![](img/d61019b035dd82beb581604273c0ee6b_148_2.png)

![](img/d61019b035dd82beb581604273c0ee6b_148_3.png)

### Implement complex decisions that require multiple if statements.
- Multiple alternatives are required for decisions that have more than two cases.
- When using multiple if statements, pay attention to the order of the conditions.

![](img/d61019b035dd82beb581604273c0ee6b_148_4.png)

### Implement decisions whose branches require further decisions.
- When a decision statement is contained inside the branch of another decision statement, the statements are nested.
- Nested decisions are required for problems that have two levels of decision making.

![](img/d61019b035dd82beb581604273c0ee6b_148_5.png)

### Draw flowcharts for visualizing the control flow of a program.
- Flowcharts are made up of elements for tasks, input/outputs, and decisions.
- Each branch of a decision can contain tasks and further decisions.
- Never point an arrow inside another branch.

![](img/d61019b035dd82beb581604273c0ee6b_149_0.png)

### Design test cases for your programs.
- Each branch of your program should be covered by a test case.
- It is a good idea to design test cases before implementing a program.

### Use the Boolean data type to store and combine conditions that can be true or false.
![](img/d61019b035dd82beb581604273c0ee6b_149_1.png)
- The Boolean type bool has two values, false and true.
- C++ has two Boolean operators that combine conditions: && (and) and || (or).
- To invert a condition, use the ! (not) operator.
- The && and || operators are computed using short-circuit evaluation: As soon as the truth value is determined, no further conditions are evaluated.
- De Morgan's Law tells you how to negate && and || conditions.

### Apply if statements to detect whether user input is valid.
![](img/d61019b035dd82beb581604273c0ee6b_149_2.png)
- When reading a value, check that it is within the required range.
- Use the fail function to test whether the input stream has failed.

## REVIEW EXERCISES

### R3.1 What is the value of each variable after the if statement?
```
a. int n = 1; int k = 2; int r = n;
if (k < n) { r = k; }
```
```
b. int n = 1; int k = 2; int r;
if (n < k) { r = k; }
else { r = k + n; }
```
```
c. int n = 1; int k = 2; int r = k;
if (r < k) { n = r * 2; }
else { k = n; }
```
```
d. int n = 1; int k = 2; int r = 3;
if (r < n + k) { r = 2 * n; }
else { k = 2 * r; }
```

### R3.2 Explain the difference between
```
s = 0;
if (x > 0) { s++; }
if (y > 0) { s++; }
```
```
s = 0;
if (x > 0) { s++; }
else if (y > 0) { s++; }
```

### R3.3 Find the errors in the following if statements.
```
a. if x > 0 then cout << x;
```
```
b. if (x > 0) { y = 1; } else { y = -1; }
```
```
c. if (1 + x > pow(x, sqrt(2))) { y = y + x; }
```
```
d. if (x == 1) { y++; }
```
```
e. cin >> x; if (cin.fail()) { y = y + x; }
```

### R3.4 What do these code fragments print?

### R3.5 Suppose x and y are variables of type double. Write a code fragment that sets y to x if x is positive and to 0 otherwise.

### R3.6 Suppose x and y are variables of type double. Write a code fragment that sets y to the absolute value of x without calling the abs function. Use an if statement.

### R3.7 Explain why it is more difficult to compare floating-point numbers than integers. Write C++ code to test whether an integer n equals 10 and whether a floating-point number x equals 10.

### R3.8
Common Error 3.2 explains that a C++ compiler will not report an error when you use an assignment operator instead of a test for equality, but it may issue a warning. Write a test program containing a statement
```
if (floor = 13)
```
What does your compiler do when you compile the program?

### R3.9
Given two pixels on a computer screen with integer coordinates (x1,y1) and (x2,y2), write conditions to test whether they are
- a. The same pixel.
- b. Very close together (with distance < 5).

### R3.10
It is easy to confuse the = and == operators. Write a test program containing the statement
```
if (floor = 13)
```
What error message do you get? Write another test program containing the statement
```
count == 0;
```
What does your compiler do when you compile the program?

### R3.11
Each square on a chess board can be described by a letter and number, such as g5 in this example:

![](img/d61019b035dd82beb581604273c0ee6b_151_0.png)

The following pseudocode describes an algorithm that determines whether a square with a given letter and number is dark (black) or light (white).
```
If the letter is an a, c, e, or g
  if the number is odd
    color = "black"
  Else
    color = "white"
Else
  if the number is even
    color = "black"
  Else
    color = "white"
```
Using the procedure in Programming Tip 3.6, trace this pseudocode with input g5.

### R3.12
Give a set of four test cases for the algorithm of Exercise R3.11 that covers all branches.
