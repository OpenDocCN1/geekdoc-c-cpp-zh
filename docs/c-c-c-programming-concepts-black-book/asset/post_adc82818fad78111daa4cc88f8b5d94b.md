
Note that in the preceding program, each case is followed by a break statement. Although, we learn about the break statement later in the chapter, let’s see what happens if we do not give the break statements in the preceding program, as follows:

```cpp
1:// Demonstrating "switch case" in C++
2:#include <iostream>
3:using namespace std;
4:
5:int main ()
6:{
7: int num;
8: cout<<"Enter a number (11/22/33): ";
9: cin >> num;
10: switch (num) {
11:    case 11:
12:        cout<<"Congratulations. You have entered 11."<<endl;
13:    case 22:
14:        cout<<"Congratulations. You have entered 22."<<endl;
15:    case 33:
16:        cout<<"Congratulations. You have entered 33."<<endl;
17:    default:
18:        cout<<"You have entered a wrong option."<<endl;
19: }
20: return 0;
21:}
```

Following is the output of the preceding program:

```text
Enter a number: 11
Congratulations. You have entered 11.
Congratulations. You have entered 22.
Congratulations. You have entered 33.
You have entered a wrong option.
```

If the break statement is not used within the switch block, the execution starts from the matched case and all the statements following that case are executed until a break is encountered or the switch block ends.

Let’s now learn about the various types of loops in C++.

## Loops

Loops cause a section of a program to be repeated a certain number of times. The repetition continues till some condition is true, based on which the looping is performed. When the condition becomes false, the loop ends, and the control passes to the statements immediately following the loop. In this section, we learn about the while, for, and do-while loops.

### The while Loop

The while loop consists of a block of code and a condition. The condition is evaluated, and if the condition is true, the code within the block is executed. This repeats until the condition becomes false. Following is the basic structure of the while loop:

```cpp
while (condition is not true) {
    //execute some statements in a loop
}
```

Before entering the while loop, condition is checked and if the condition is found true, then the statements inside the while loop are executed. Now, after each round of condition validation, the program control goes over all the statements in a while block, again the condition is checked and similar procedure is followed if the condition is found true. Otherwise, the program flow exits the while loop and starts executing the instructions following the while loop. Listing 12.5 shows the flow of while loop in C++:

**Listing 12.5:** Displaying the Flow of while Loop

```cpp
1: // Demonstrating the flow of "while loop" in C++
2: #include <iostream>
3: using namespace std;
4:
5: int main ()
6: {
7:     int num = 0;
8:     while (num != -1) {
9:         cout << "Enter a number: ";
10:        cin >> num;
11:    }
12:    return 0;
13: }
```

In Listing 12.5, we prompt a user to input a number, which is consumed by the program until and unless the user inputs -1. Whenever the user enters -1, the program ends its execution.

Following is the output of the preceding program:

```text
Enter a number: 12
Enter a number: 23
Enter a number: 125
Enter a number: 312
Enter a number: 92
Enter a number: 10
Enter a number: -1
```

While loops can also be used for doing comparisons in searching and sorting, where from the beginning, we do not know how many times to loop on the condition.

### The for Loop

The for loop is the most popular looping construct in C++. This loop executes a set of code for a fixed number of times. It is used for situations where we can determine the number of times that a loop will execute. The for loop consists of a keyword for, followed by a pair of parentheses that contain three expressions separated by semicolon. These are the expressions are initialization, test condition, and increment or decrement operation. Following is the example that shows the three expressions:

```cpp
for (i=1; i< 21; i++)
```

In the preceding example, the initialization expression is i=1, test condition is i<21 based on which the for loop works and the increment operation is i++. These are expressions that contain three expressions but (not always) involve the same variable which is called the loop variable. In our case, it is i, which should be defined before the for body starts executing. Alternatively, we can also define i in the for loop statement as follows:

```cpp
for (int i=1; i< 21; i++)
```

The body of the for loop is a set of statements to be executed each time through the loop. At the beginning of the loop, for executes the initialization expression and then checks for the validity of the test condition. If the test condition is found invalid, the flow breaks from the for loop. However, if the test condition is true, the for loop executes the loop body once, and then executes the increment or decrement statement, and again checks for the test condition before executing the body of the loop. This way, the execution of the for loop continues until the test condition is true.

Let’s now write a program to show the working of the for loop. Following program prints the square of numbers from 1 to 20 using the for loop:

```cpp
1: // Demonstrating "for loop" in C++
2: #include <iostream>
3: using namespace std;
4:
5: int main ()
6: {
7: int i;
8: for (i=1; i < 21; i++) {
9:     cout <<"Square of "<<i<<" is "<<i*i<<endl;
10: }
11:     return 0;
12:}
```

In the preceding program, the for loop body contains a single statement for calculating and displaying the square of numbers.

Following is the output of the preceding program:

```text
Square of 1 is 1
Square of 2 is 4
Square of 3 is 9
Square of 4 is 16
Square of 5 is 25
Square of 6 is 36
Square of 7 is 49
Square of 8 is 64
Square of 9 is 81
Square of 10 is 100
Square of 11 is 121
Square of 12 is 144
Square of 13 is 169
Square of 14 is 196
Square of 15 is 225
Square of 16 is 256
Square of 17 is 289
Square of 18 is 324
Square of 19 is 361
Square of 20 is 400
```

Let’s now learn about the do-while loop.

### The do-while Loop

In the while loop, the test condition is evaluated at the beginning of the loop. If the test condition is false, then the program control does not enter into the loop body and the statements would not execute even once. In some situations, we need to have this specific requirement. Sometimes, however, we need to guarantee that the loop body is executed at least once irrespective of the condition. In this case, we should use the do-while loop, which places the test condition at the end of the loop. Following program shows the use of the do-while loop:

```cpp
1:// Demonstrating "do-while loop" in C++
2:#include <iostream>
3:using namespace std;
4:
5:int main ()
6:{
7:int a, b, c;
8: char ch;
9: do {
10:         cout <<"\nEnter a number: ";
11:         cin >> a;
12:         cout <<"Enter another number: ";
13:         cin >> b;
14:         cout <<"The sum of "<<a<<" and "<<b<<" is "<<a+b<<endl;
15:         cout <<"Do you want to continue? (y/n) ";
16:         cin >> ch;
17: } while (ch != 'n');
18:     return 0;
19:}
```

In the preceding program, we take two numbers from a user as input, add the numbers, and then display the result on the screen. This process continues until the user stops it. In other words, the user is allowed to enter the numbers and prompted to continue. The program can be terminated on pressing the n key, else it will keep on absorbing inputs from the user. Following is the output of the preceding program:

```text
Enter a number: 9
Enter another number: 10
The sum of 9 and 10 is 19
Do you want to continue? (y/n) y

Enter a number: 45
Enter another number: 6
The sum of 45 and 6 is 51
Do you want to continue? (y/n) n
```

Let’s now learn about jump statements.

## Jump Statements

Jump statements cause a conditional or unconditional, but immediate jump to another statement, which is located somewhere else in the program. They are primarily used to interrupt switch statements and loops. In the following sections, we discuss about three types of jump statements: break, continue, and goto.

### The break Statement

As already learned, the break statement is used after each case within the switch block. However, the break statement is also used within the while and for loops to jump or break out of the loop based on some conditional values in the loop. The break keyword causes to break the control of the program to jump out of the currently executing loop. Consider the following program:

```cpp
1:// Demonstrating the break statement in C++
2:#include <iostream>
3:using namespace std;
4:
5:int main ()
6:{
7:for (int i=0; i<10; i++) {
8:    if (i == 7) {
9:        cout <<"Aborting the for loop."<<endl;
10:        break;
11:    }
12:    cout <<"The current value of i is "<<i<<endl;
13:}
14:
15:    return 0;
16:}
```

In line number 8, the break statement is used to jump out of the for loop as soon as the value of loop variable becomes 7. The output of the preceding program is as follows.

```text
The current value of i is 0
The current value of i is 1
The current value of i is 2
The current value of i is 3
The current value of i is 4
The current value of i is 5
The current value of i is 6
Aborting the for loop.
```

Let’s now learn about the continue statement.
