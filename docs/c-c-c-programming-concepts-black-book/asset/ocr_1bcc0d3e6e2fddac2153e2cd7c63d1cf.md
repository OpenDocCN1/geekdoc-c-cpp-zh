Note that in the preceding program, each case is followed by a break statement. Although, we learn about the break statement later in the chapter, let’s see what happens if we do not give the break statements in the preceding program, as follows:

```
~~~cpp
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
~~~
```

Following is the output of the preceding program:

```
~~~text
Enter a number: 11
Congratulations. You have entered 11.
Congratulations. You have entered 22.
Congratulations. You have entered 33.
You have entered a wrong option.
~~~
```

If the break statement is not used within the switch block, the execution starts from the matched case and all the statements following that case are executed until a break is encountered or the switch block ends.

Let’s now learn about the various types of loops in C++.

# ### Loops

Loops cause a section of a program to be repeated a certain number of times. The repetition continues till some condition is true, based on which the looping is performed. When the condition becomes false, the loop ends, and the control passes to the statements immediately following the loop. In this section, we learn about the while, for, and do-while loops.

# ### The while Loop

The while loop consists of a block of code and a condition. The condition is evaluated, and if the condition is true, the code within the block is executed. This repeats until the condition becomes false. Following is the basic structure of the while loop:

```
~~~cpp
while (condition is not true) {
    //execute some statements in a loop
}
~~~
```

Before entering the while loop, condition is checked and if the condition is found true, then the statements inside the while loop are executed. Now, after each round of condition validation, the program control goes over all the statements in a while block, again the condition is checked and similar procedure is followed if the condition is found true. Otherwise, the program flow exits the while loop and starts executing the instructions following the while loop. Listing 12.5 shows the flow of while loop in C++: