
scale rand with the remainder operator (i.e., % 6), and the starting number of the range is equal to the number (i.e., 1) that’s added to rand % 6. We can generalize this result as follows:

```
int n = a + rand() % b;
```

- **a** is the shifting value (which is equal to the first number in the desired range of consecutive integers), and
- **b** is the *scaling factor* (which is equal to the width of the desired range of consecutive integers).

In the exercises, you’ll choose integers at random from sets of values other than ranges of consecutive integers.

![](img/43d318ad505997c339a3ea78d716d162_257_0.png)

## Self Check

1. **(Fill-In)** __________ is an important characteristic of function rand. When we’re debugging a program, this characteristic is essential for proving that corrections to a program work properly.  
   **Answer:** Repeatability.

2. **(True/False)** If rand truly produces integers at random, every number between 0 and RAND_MAX has an equal chance (or probability) of being chosen each time rand is called.  
   **Answer:** *True.*

3. **(Fill-In)** Once a program has been thoroughly debugged, it can be conditioned to produce a different sequence of random numbers for each execution. This is called randomizing and is accomplished with the standard library function ________.  
   **Answer:** srand.

## 5.11 Random-Number Simulation Case Study: Building a Casino Game

In this section, we simulate the popular dice game known as “craps.” The rules of the game are straightforward:

> A player rolls two dice. Each die has six faces. These faces contain 1, 2, 3, 4, 5, and 6 spots. After the dice have come to rest, the sum of the spots on the two upward faces is calculated. If the sum is 7 or 11 on the first throw, the player wins. If the sum is 2, 3, or 12 on the first throw (called “craps”), the player loses (i.e., the “house” wins). If the sum is 4, 5, 6, 8, 9, or 10 on the first throw, that sum becomes the player’s “point.” To win, you must continue rolling the dice until you “make your point.” The player loses by rolling a 7 before making the point.

Figure 5.7 simulates the game of craps and shows several sample executions.

```c
// fig05_07.c
// Simulating the game of craps.
#include <stdio.h>
#include <stdlib.h>
#include <time.h> // contains prototype for function time

enum Status {CONTINUE, WON, LOST}; // constants represent game status

int rollDice(void); // rollDice function prototype

int main(void) {
    srand(time(NULL)); // randomize based on current time

    int myPoint = 0; // player must make this point to win
    enum Status gameStatus = CONTINUE; // may be CONTINUE, WON, or LOST
    int sum = rollDice(); // first roll of the dice

    // determine game status based on sum of dice
    switch(sum) {
        // win on first roll
        case 7: // 7 is a winner
        case 11: // 11 is a winner
            gameStatus = WON;
            break;
        // lose on first roll
        case 2: // 2 is a loser
        case 3: // 3 is a loser
        case 12: // 12 is a loser
            gameStatus = LOST;
            break;
        // remember point
        default:
            gameStatus = CONTINUE; // player should keep rolling
            myPoint = sum; // remember the point
            printf("Point is %d\n", myPoint);
            break; // optional
    }

    // while game not complete
    while (CONTINUE == gameStatus) { // player should keep rolling
        sum = rollDice(); // roll dice again

        // determine game status
        if (sum == myPoint) { // win by making point
            gameStatus = WON;
        }
        else if (7 == sum) { // lose by rolling 7
            gameStatus = LOST;
        }
    }

    // display won or lost message
    if (WON == gameStatus) { // did player win?
        puts("Player wins");
    } else { // player lost
        puts("Player loses");
    }
}

// roll dice, calculate sum and display results
int rollDice(void) {
    int die1 = 1 + (rand() % 6); // pick random die1 value
    int die2 = 1 + (rand() % 6); // pick random die2 value

    // display results of this roll
    printf("Player rolled %d + %d = %d\n", die1, die2, die1 + die2);
    return die1 + die2; // return sum of dice
}
```

*Fig. 5.7 | Simulating the game of craps. (Part 1 of 2.)*

**Player wins on the first roll:**

```
Player rolled 5 + 6 = 11
Player wins
```

**Player wins on a subsequent roll:**

```
Player rolled 4 + 1 = 5
Point is 5
Player rolled 6 + 2 = 8
Player rolled 2 + 1 = 3
Player rolled 3 + 2 = 5
Player wins
```

**Player loses on the first roll:**

```
Player rolled 1 + 1 = 2
Player loses
```

**Player loses on a subsequent roll:**

```
Player rolled 6 + 4 = 10
Point is 10
Player rolled 3 + 4 = 7
Player loses
```

*Fig. 5.7 | Simulating the game of craps. (Part 2 of 2.)*

In the game, the player must roll two dice on each roll. We define the rollDice function to roll the dice and compute and print their sum. The function is defined once, but it’s called twice (lines 16 and 41). The function takes no arguments, so we’ve indicated void in the parameter list (line 62) and the function prototype (line 9). Function rollDice does return the sum of the two dice, so a return type of int is indicated in its function header and in its function prototype.

### Enumerations

The game is reasonably involved. The player may win or lose on the first roll or any subsequent roll. Variable gameStatus, defined to be of a new type—enum Status—stores the current status. Line 7 creates a new type called an enumeration. An enumeration, introduced by the keyword enum, is a set of integer constants represented by identifiers. Enumeration constants help make programs more readable and easier to maintain. Values in an enum start with 0 and are incremented by 1. In line 7, the constant CONTINUE has the value 0, WON has the value 1 and LOST has the value 2. It's also possible to assign an integer value to each identifier in an enum (see Chapter 10). The identifiers in an enumeration must be unique, but the values may be duplicated. Use only uppercase letters in enum constant names to make them stand out in a program and to indicate they are not variables.

When the game is won, gameStatus is set to WON. When the game is lost, gameStatus is set to LOST. Otherwise, gameStatus is set to CONTINUE, and the game continues.

### Game Ends on First Roll

If the game is over after the first roll, gameStatus is not CONTINUE, so the program proceeds to the if...else statement at lines 53–58, which prints "Player wins" if gameStatus is WON and "Player loses" otherwise.

### Game Ends on a Subsequent Roll

After the first roll, if the game is not over, then sum is saved in myPoint. Execution proceeds with the while statement because gameStatus is CONTINUE. Each time through the while, rollDice is called to produce a new sum:

- If sum matches myPoint, gameStatus is set to WON, the while loop terminates, the if...else statement prints "Player wins" and execution terminates.
- If sum is 7 (line 47), gameStatus is set to LOST, the while loop terminates, the if...else statement prints "Player loses" and execution terminates.

### Control Architecture

Note the program's control architecture. We've used two functions—main and rollDice—and the switch, while and nested if...else statements.

### Related Exercises

This Building a Casino Game case study is supported by the following exercises:

- Exercise 5.47 (Craps Game Modification).
- Exercise 6.20 (Craps Game Statistics).

## Self Check

1. (Fill-In) An enumeration, introduced by the keyword _______, is a set of integer constants represented by identifiers.  
   **Answer:** enum.

2. (Fill-In) In the following statement

   ```
   enum Status {CONTINUE, WON, LOST};
   ```

   the values of CONTINUE, WON and LOST are _______, _______ and _______.  
   **Answer:** 0, 1 and 2.

## 5.12 Storage Classes

In Chapters 2–4, we used identifiers for variable names. The attributes of variables include name, type, size and value. In this chapter, we also use identifiers as names for user-defined functions. Actually, each identifier in a program has other attributes, including storage class, storage duration, scope and linkage.

C provides the storage-class specifiers auto, register, extern and static. A storage class determines an identifier’s storage duration, scope and linkage. Storage duration is the period during which an identifier exists in memory. Some exist briefly, some are repeatedly created and destroyed, and others exist for the entire program execution. Scope determines where a program can reference an identifier. Some can be referenced throughout a program, others from only portions of a program. For a multiple-source-file program, an identifier’s linkage determines whether the identifier is known only in the current source file or in any source file with proper declarations. This section discusses storage classes and storage duration, and Section 5.13 discusses scope. Chapter 15 discusses identifier linkage and programming with multiple source files.

### Local Variables and Automatic Storage Duration

The storage-class specifiers are split between automatic storage duration and static storage duration. The auto keyword declares that a variable has automatic storage duration. Such variables are created when program control enters the block in which they’re defined. They exist while the block is active, and they’re destroyed when program control exits the block.

Only variables can have automatic storage duration. A function’s local variables—those declared in the parameter list or function body—have automatic storage duration by default, so the auto keyword is rarely used. Automatic storage duration is a means of conserving memory because local variables exist only when they’re needed. We’ll refer to variables with automatic storage duration simply as local variables.

### Static Storage Class

Keywords extern and static declare identifiers for variables and functions with static storage duration. Identifiers of static storage duration exist from the time at which the program begins execution until it terminates. For static variables, storage is allocated and initialized only once, before the program begins execution. For functions, the name of the function exists when the program begins execution. However, even though these names exist from the start of program execution, they are not always
