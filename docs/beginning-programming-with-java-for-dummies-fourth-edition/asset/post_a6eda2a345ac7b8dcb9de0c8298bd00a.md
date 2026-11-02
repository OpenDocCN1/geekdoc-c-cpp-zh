
### Listing 10-7 (continued)

```java
if (hankees > socks) {
    who = WhoWins.home;
    out.println("The Hankees win :-)");
} else if (socks > hankees) {
    who = WhoWins.visitor;
    out.println("The Socks win :-(");
} else {
    who = WhoWins.neither;
    out.println("It's a tie :-|");
}

out.println();
out.println("Today's game is brought to you by");
out.println("SnitSoft, the number one software");
out.println("vendor in the Hankeeville area.");
out.println("SnitSoft is featured proudly in");
out.println("Chapter 6. And remember, four out");
out.println("of five doctors recommend");
out.println("SnitSoft to their patients.");
out.println();

if (who == WhoWins.home) {
    out.println("We beat 'em good. Didn't we?");
}

if (who == WhoWins.visitor) {
    out.println("The umpire made an unfair");
    out.println("call.");
}

if (who == WhoWins.neither) {
    out.println("The game goes into overtime.");
}

keyboard.close();
}
```

Three runs of the program in Listing 10-7 are pictured in Figure 10-13.

### Figure 10-13: Joy in Hankeeville?

```
Hankees and Socks scores? 9 4

The Hankees win :-)

Today's game is brought to you by SnitSoft, the number one software vendor in the Hankeeville area.
SnitSoft is featured proudly in Chapter 6. And remember, four out of five doctors recommend SnitSoft to their patients.

We beat 'em good. Didn't we?

Hankees and Socks scores? 3 8

The Socks win :-( 

Today's game is brought to you by SnitSoft, the number one software vendor in the Hankeeville area.
SnitSoft is featured proudly in Chapter 6. And remember, four out of five doctors recommend SnitSoft to their patients.

The umpire made an unfair call.

Hankees and Socks scores? 0 0

It's a tie :-|

Today's game is brought to you by SnitSoft, the number one software vendor in the Hankeeville area.
SnitSoft is featured proudly in Chapter 6. And remember, four out of five doctors recommend SnitSoft to their patients.

The game goes into overtime.
```

Here's what happens in Listing 10-7:

- ✓ I create a variable to store values of type WhoWins.
- Just as the line `double amount;` declares amount to store double values (values like 5.95 and 30.95), the line `WhoWins who;` declares who to store WhoWins values (values like home, visitor, and neither).
- ✓ I assign a value to the who variable. I execute one of the `who = WhoWins.something;` assignment statements. The statement that I execute depends on the outcome of the if statement's hankees > socks comparison.

Notice that I refer to each of the WhoWins values in Listing 10-7. I write WhoWins.home, WhoWins.visitor, or WhoWins.neither. If I forget the WhoWins prefix and type

```
who = home; //This assignment doesn't work!
```

the compiler gives me a home cannot be resolved to a variable error message. That's just the way enum types work.

- ✓ I compare the variable's value with each of the WhoWins values.

In one if statement, I check the who == WhoWins.home condition. In the remaining two if statements, I check for the other WhoWins values.

Near the end of Listing 10-7, I could have done without enum values. I could have tested things like hankees > socks a second time.

```
if (hankees > socks) {
    out.println("The Hankees win :-)");
}

// And later in the program...

if (hankees > socks) {
    out.println("We beat 'em good. Didn't we?");
}
```

But that tactic would be clumsy. In a more complicated program, I may end up checking hankees > socks a dozen times. It would be like asking the same question over and over again.

Instead of repeatedly checking the hankees > socks condition, I store the game's outcome as an enum value. Then I check the enum value as many times as I want. That's a very tidy way to solve the repeated checking problem.

## Chapter 11: How to Flick a Virtual Switch

### In This Chapter

- Dealing with many alternatives
- Jumping out from the middle of a statement
- Handling alternative assignments

Imagine playing Let's Make a Deal with ten different doors. "Choose door number 1, door number 2, door number 3, door number 4 . . . Wait! Let's break for a commercial. When we come back, I'll say the names of the other six doors."

What Monty Hall needs is Java's switch statement.

### Meet the switch Statement

The code in Listing 9-2 in Chapter 9 simulates a fortune-telling toy — an electronic oracle. Ask the program a question, and the program randomly generates a yes or no answer. But, as toys go, the code in Listing 9-2 isn't much fun. The code has only two possible answers. There's no variety. Even the earliest talking dolls could say about ten different sentences.

Suppose that you want to enhance the code of Listing 9-2. The call to myRandom.nextInt(10) + 1 generates numbers from 1 to 10. So maybe you can display a different sentence for each of the ten numbers. A big pile of if statements should do the trick:

```java
if (randomNumber == 1) {
    System.out.println("Yes. Isn't it obvious?");
}
if (randomNumber == 2) {
    System.out.println("No, and don't ask again.");
}
if (randomNumber == 3) {
    System.out.print("Yessir, yessir!");
    System.out.println(" Three bags full.");
}
if (randomNumber == 4)
  ...
if (randomNumber < 1 || randomNumber > 10) {
    System.out.print("Sorry, the electronic oracle");
    System.out.println(" is closed for repairs.");
}
```

But that approach seems wasteful. Why not create a statement that checks the value of randomNumber just once and then takes an action based on the value that it finds? Fortunately, just such a statement exists: the switch statement. Listing 11-1 has an example of a switch statement.

### Listing 11-1: An Answer for Every Occasion

```java
import java.util.Scanner;
import java.util.Random;
import static java.lang.System.out;

class TheOldSwitcheroo {

    public static void main(String args[]) {
        Scanner keyboard = new Scanner(System.in);
        Random myRandom = new Random();
        int randomNumber;

        out.print("Type your question, my child: ");
        keyboard.nextLine();

        randomNumber = myRandom.nextInt(10) + 1;

        switch (randomNumber) {
        case 1:
            out.println("Yes. Isn't it obvious?");
            break;

        case 2:
            out.println("No, and don't ask again.");
            break;

        case 3:
            out.print("Yessir, yessir!");
            out.println(" Three bags full.");
            break;

        case 4:
            out.print("What part of 'no'");
            out.println(" don't you understand?");
            break;

        case 5:
            out.println("No chance, Lance.");
            break;

        case 6:
            out.println("Sure, whatever.");
            break;

        case 7:
            out.print("Yes, but only if");
            out.println(" you're nice to me.");
            break;

        case 8:
            out.println("Yes (as if I care).");
            break;

        case 9:
            out.print("No, not until");
            out.println(" Cromwell seizes Dover.");
            break;

        case 10:
            out.print("No, not until");
            out.println(" Nell squeezes Rover.");
            break;

        default:
            out.print("You think you have");
            out.print(" problems?");
            out.print(" My random number");
            out.println(" generator is broken!");
            break;
        }

        out.println("Goodbye");
        keyboard.close();
    }
}
```

![](img/6d9dcff12e52b997f3ad31445b712549_236_0.png)

### Figure 11-2: A fork with 11 prongs.

### The default in a switch statement

What if something goes terribly wrong during a run of the Listing 11-1 program? Suppose that the expression `myRandom.nextInt(10) + 1` generates a number that’s not in the 1 to 10 range. Then the computer responds by dropping past all the case clauses. Instead of landing on a case clause, the computer jumps to the default clause. In the default clause, the computer displays `You think you have problems?...`, and then breaks out of the switch statement. After the computer is out of the switch statement, the computer displays Goodbye.

![](img/6d9dcff12e52b997f3ad31445b712549_236_1.png)

You don’t really need to put a break at the very end of a switch statement. In Listing 11-1, the last break (the break that’s part of the default clause) is just for the sake of overall tidiness.
