
## CHAPTER 7 The Repetition Structure

| Input | Processing | Output |
| :--- | :--- | :--- |
| score (5 of them) | Processing items: none | total points earned grade |

```
Algorithm:
1. enter the first score
  repeat while (the score is not -1)
    add the score to the total points earned
    enter the next score
  end repeat
3. if (the total points earned >= 315)
    assign A as the grade
  else if (the total points earned >= 280)
    assign B as the grade
  else if (the total points earned >= 245)
    assign C as the grade
  else if (the total points earned >= 210)
    assign D as the grade
  else
    assign F as the grade
  end if
4. display the total points earned and the grade
```

Figure 7-44 Completed IPO chart for the Professor Chang problem

After completing the IPO, you then move to the third step in the problem-solving process, which is to desk-check the algorithm. You will desk-check the algorithm in Figure 7-44 twice. For the first desk-check, you will use the following five scores and sentinel value: 45, 40, 41, 96, 89, and -1. You will use the following five scores and sentinel value for the second desk-check: 40, 35, 37, 73, 68, and -1. Figure 7-45 shows the completed desk-check table. Notice that the values in the total points earned and grade columns agree with the results of the manual calculations in Figure 7-43.

| | total points earned | grade |
| :--- | :--- | :--- |
| 45 | 45 | |
| 40 | 55 | |
| 41 | 120 | |
| 96 | 288 | |
| 89 | 311 | B |
| -1 | | |
| 40 | 40 | |
| 35 | 75 | |
| 37 | 112 | |
| 73 | 155 | |
| 68 | 253 | C |
| -1 | | |

Figure 7-45 Completed desk-check table for the Professor Chang algorithm

## The for Statement

The fourth step in the problem-solving process is to code the algorithm into a program. You begin by declaring memory locations that will store the values of the input, processing (if any), and output. The Professor Chang problem will need memory locations to store the input and output items. The input item (score) will be stored in a variable, because the user should be allowed to change its value during running. The output items (total points earned and grade) will also be stored in variables, because their values will change based on the current value of the input item. The score and total points earned will always be integers, so you will store both in variables. You will store the grade in a char variable. Figure 7-46 shows the IPO chart information and corresponding C++ instructions.

Figure 7-46 IPO chart information and C++ instructions for Professor Chang program

The fifth step in the problem-solving process is to desk-check the program. You begin by placing the names of declared variables and named constants (if any) in a new desk-check table with their initial values. Then desk-check the remaining instructions in order, recording desk-check changes made to the variables. Figure 7-47 shows the completed desk-check table for Professor Chang program. The results agree with those shown in the algorithm's desk-check table in Figure 7-45.

Figure 7-47 Completed desk-check table for Professor Chang program

The final step in the problem-solving process is to evaluate and modify (if necessary) the program. Recall that you evaluate a program by entering its instructions into the computer and then using the computer to run (execute) it. While the program is running, you enter the sample data used when desk-checking the program.

# DIRECTIONS

Follow the instructions for starting your C++ development tool. Depending on development tool you are using, you may need to create a new project; if so, name the project Lab7-2 and save it in the Chapter 7 folder. (Do not enter the same name). Save the file in the project folder or Chapter 7 folder. Now follow the instructions for running the Lab7-2.cpp file. Use the sample data from Figure 7-45 to test the program. If necessary, correct any bugs (errors) in the program.

```
// Lab7-2.cpp displays total points earned and grade
// revised by <your name> on <current date>
#include <iostream>

using namespace std;

int main()
{
    // declare variables
    int score = 0;
    int totalPoints = 0; //accumulator
    char grade = ' ';

    // get first score
    cout << "First score (-1 to stop): ";
    cin >> score;

    while (score != -1)
    {
        // update accumulator, then another score
        totalPoints += score;
        cout << "Next score (-1 to stop): ";
        cin >> score;
    } //end while

    // determine grade
    if (totalPoints >= 315)
        grade = 'A';
    else if (totalPoints >= 280)
        grade = 'B';
    else if (totalPoints >= 245)
        grade = 'C';
    else if (totalPoints >= 210)
        grade = 'D';
    else
        grade = 'F';
    } //end if

    // display the total points and grade
    cout << "Points earned: " << totalPoints << endl;
    cout << "Grade: " << grade << endl;

    system("pause");
    return 0;
}//end of main function
```

> your C++ development tool may not require this statement

Figure 7-48 Professor Chang program (continued)

![](img/d64a28a68f49d6137bf2f3170ac40ad_267_0.png)

## LAB 7-3 Modify

If necessary, create a new project Lab7-3. Enter (or copy) the Lab7-2.cpp instructions into a new source file named Lab7-3.cpp. Change Lab7-2. Professor Chang now wants the program to display the total number of scores he enters. Modify the program appropriately, and then save and run the program. Test the program using the five scores and sentinel value: 45, 40, 41, 96, 98, and -1. The total points earned and grade should be 315 and B, respectively. In addition, the program should indicate that Professor Chang entered 5 scores. Now test the program a second time using the following scores and sentinel value: 25, 500 (Professor Chang suddenly enters 500 rather than 50), 38, -500 (Professor Chang corrects his mistake by entering a negative number 500), 50, 64, 78, and -1. Does the program display the correct total points earned and grade? How many scores does the program indicate that Professor Chang entered?

![](img/d64a28a68f49d6137bf2f3170ac40ad_268_0.png)

## LAB 7-4 Desk-Check

The code shown in Figure 7-49 should display the squares of the numbers from 1 through 5. In other words, it should display the numbers 1, 4, 9, 16, and 25. Did your desk-check reveal any errors in the code? If so, correct the code and then desk-check it.

```
// declare variables
int squaredNumber = 0;
for (int number = 1; number < 5; number = number + 1)
{
    squaredNumber = number * number;
    cout << squaredNumber << endl;
}//end for
```

Figure 7-49 Code for Lab 7

![](img/d64a28a68f49d6137bf2f3170ac40ad_268_1.png)

## LAB 7-5 Debug

FollowFollow the instructions for starting C++ and opening the Lab7-5.cpp file. The file is contained in the Chapter 7\Lab7-5 Project folder or Chapter 7 folder. Run the program. When you are prompted to enter a value, type 15 and press Enter. The "Next" prompt appears over and again in the Prompt window, as shown in Figure 7-50. This is the result of the computer redoing the cout "Next: "; statement, which is contained in the body of the while loop, and it indicates that the program contains an endless (infinite) loop. You can stop an endless loop by pressing Ctrl+c and hold down the Ctrl key as you tap the letter c, and then release keys. (If you are using Microsoft C++, you may need to click the Continue button after pressing Ctrl+c). Or, you can use the Close button on the Command Prompt window's title bar.
