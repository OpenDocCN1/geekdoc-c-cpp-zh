# The continue Statement

As already learned, the break statement takes the program control out of the current scope of the loop or switch case. Sometimes, however, based on the conditions within the loop, a programmer might decide that instead of going out of the loop, the program control should go to the beginning of the loop. This can be done by using the continue statement in the program. While executing the program, if a continue statement is encountered, the program control immediately goes back to the beginning of the loop without executing the rest of the loop body.

As soon as the continue statement is encountered in a program, the program will check for the test condition again and increment or decrement the loop variable again before executing the loop body. Let’s write a program to demonstrate this feature. In the following program, we are showing the usage of a continue statement by means of a for loop:

```
```cpp
1:// Demonstrating the continue statement in C++
2:#include <iostream>
3:using namespace std;
4:
5:int main ()
6:{
7:for (int i=1; i<=10; i++) {
8:    if (i == 5) {
9:        continue;
10:    }
11:    cout << "The current value of i is " << i << endl;
12:}
13:return 0;
14:}
```
```

In the following program, the for loop iterates for ten times and prints each integer number except 5, on which a continue statement is applied.

Following is the output of the preceding program:

```
```
The current value if i is 1
The current value if i is 2
The current value if i is 3
The current value if i is 4
The current value if i is 6
The current value if i is 7
The current value if i is 8
The current value if i is 9
The current value if i is 10
```
```

Let’s now learn about the goto statement.

# The goto Statement

If you have any exposure to the structured programming principles, you might know that goto can lead to a bad coding style, which is difficult to understand and debug. It is also advisable not to use goto in programs, as it makes the program unstructured, which is known as bad programming. Although we always try to adhere to the ideas of structured programming concept, yet at times it gets difficult to handle some situations without a goto statement. Assume a situation where the program control is inside a loop and based on some exception occurred, we not only want to exit the loop, but also want to skip most of the statements of the main loop and do some cleanup activities before exiting from the program. The following code snippet shows the syntax of goto:

```
```cpp
...

goto ExceptionOccurred;  // goto statement encountered
```
```