
That does it. That's all you need. The code to create the display of Figure 15-5 is in Listing 15-3.

### Listing 15-3: Hey! Is This a For-by-For?

```java
import java.util.Scanner;
import java.io.File;
import java.io.FileNotFoundException;
import static java.lang.System.out;

class DisplayHotelData {
    public static void main(String args[])
    throws FileNotFoundException {
        Scanner diskScanner =
            new Scanner(new File("hotelData"));
        for (int floor = 1; floor <= 9; floor++) {
            out.print("Floor ");
            out.print(floor);
            out.print(": ");
            for (int roomNum = 1; roomNum <= 20; roomNum++) {
                out.print(diskScanner.nextInt());
                out.print(' ');
            }
            out.println();
        }
        diskScanner.close();
    }
}
```

The code in Listing 15-3 has the variable floor going from 1 to 9 and has the variable roomNum going from 1 to 20. Because the roomNum loop is inside the floor loop, the writing of 20 numbers happens 9 times. That's good. It's exactly what I want.

## Repeating Until You Get What You Need (Java do Statements)

I introduce Java's while loop in Chapter 12. When you create a while loop, you write the loop's condition first. After the condition, you write the code that gets repeatedly executed.

```
while (Condition) {
    Code that gets repeatedly executed
}
```

This way of writing a while statement is no accident. The look of the statement emphasizes an important point — that the computer always checks the condition before executing any of the repeated code.

If the loop's condition is never true, then the stuff inside the loop is never executed — not even once. In fact, you can easily cook up a while loop whose statements are never executed (although I can't think of a reason why you would ever want to do it):

```
//This code doesn't print anything:
int twoPlusTwo = 2 + 2;
while (twoPlusTwo == 5) {
    System.out.println("Are you kidding?");
    System.out.println("2+2 doesn't equal 5.");
    System.out.print ("Everyone knows that");
    System.out.println(" 2+2 equals 3.");
}
```

In spite of this silly twoPlusTwo example, the while statement turns out to be the most useful of Java's looping constructs. In particular, the while loop is good for situations in which you must look before you leap. For example: "While money is in my account, write a mortgage check every month." When you first encounter this statement, if your account has a zero balance, you don't want to write a mortgage check — not even one check.

But at times (not many), you want to leap before you look. In a situation when you're asking the user for a response, maybe the user's response makes sense, but maybe it doesn't. Maybe the user's finger slipped, or perhaps the user didn't understand the question. In many situations, it's important to correctly interpret the user's response. If the user's response doesn't make sense, you must ask again.

### Getting a trustworthy response

Consider a program that deletes a file. Before deleting the file, the program asks for confirmation from the user. If the user types Y, then delete; if the user types N, then don't delete. Of course, deleting a file is serious stuff. Mistaking a bad keystroke for a "yes" answer can delete the company's records. (And mistaking a bad keystroke for a "no" answer can preserve the company's incriminating evidence.) So if there's any doubt about the user's response, the program should ask the user to respond again.

![](img/bf4858233d2b2a32ff4e3991860526b3_313_0.png)

### 6. Observe that the file's name appears in Eclipse's Package Explorer.

The name is in the 15-04 project's root directory. You put it in the root directory because, in Listing 15-04, the name importantData.txt (with no slashes or backslashes) refers only to a name in the project's root directory. The program's run has no effect on any files outside the root directory, even if any of those files have the name importantData.txt.

To find out how to refer to files outside of the project's root directory, refer to Chapter 13.

For this experiment, you don't have to add any text to the file. The file exists only to be deleted.

### 7. Run the program.

When the program runs, type Y to delete the importantData.txt file.

After running the program, you want to check to make sure that the program deleted the importantData.txt file.

### 8. In the Package Explorer, select the project's root (again, for good measure).

### 9. In Eclipse's main menu, choose File→Refresh.

Eclipse takes another look at the project directory and lists the directory's files in the Package Explorer's tree. Assuming that the program did its job correctly, the file named importantData.txt no longer appears in the tree.

In Listing 15-4, the statement

```
new File("importantData.txt").delete();
```

is tricky. At first glance, you seem to be creating a new file, only to delete that file in the same line of code! But in reality, the words new File create only a representation of a file inside your program. To be more precise, the words new File create, inside your program, a representation of a disk file that may or may not already exist on your computer's hard drive. So here's what the new File statement really means:

> "Let new File("importantData.txt") refer to a file named importantData.txt. If such a file exists, then delete it."

Yes, the devil is in the details. But smiles are in the subtleties and nobility is in the nuance.

## Using Java's do statement

To write the program in Listing 15-4, you need a loop — a loop that repeatedly asks the user whether the importantData.txt file should be deleted. (The action of the loop in Listing 15-4 is illustrated in Figure 15-7.) The loop continues to ask until the user gives a meaningful response. The loop tests its condition at the end of each iteration, after each of the user's responses.

![](img/bf4858233d2b2a32ff4e3991860526b3_314_0.png)

Figure 15-7:
Here we
go loop, do
loop.

That's why the program in Listing 15-4 has a do loop (also known as a do... while loop). With a do loop, the program jumps right in, executes some statements, and then checks a condition. If the condition is true, the program goes back to the top of the loop for another go-around. If the condition is false, the computer leaves the loop (and jumps to whatever code comes immediately after the loop).

### A closer look at the do statement

The format of a do loop is

```
do {
    Statements
} while (Condition)
```

Writing the Condition at the end of the loop reminds me that the computer executes the Statement inside the loop first. After the computer executes the Statement, the computer goes on to check the Condition. If the Condition is true, the computer goes back for another iteration of the Statement.

With a do loop, the computer always executes the statements inside the loop at least once:

```
//This code prints something:
int twoPlusTwo = 2 + 2;
do {
    System.out.println("Are you kidding?");
    System.out.println("2+2 doesn't equal 5.");
    System.out.print("Everyone knows that");
    System.out.println(" 2+2 equals 3.");
} while (twoPlusTwo == 5);
```

This code displays Are you kidding? 2+2 doesn't equal 5... and so on and then tests the condition twoPlusTwo == 5. Because twoPlusTwo == 5 is false, the computer doesn't go back for another iteration. Instead, the computer jumps to whatever code comes immediately after the loop.

## Repeating with Predetermined Values (Java's Enhanced for Statement)

Most people say that they "never win anything." Other people win raffles, drawings, and contests, but they don't win things. Well, I have news for these people — other people don't win things, either. Nobody wins things. That's how the laws of probability work. Your chance of winning one of the popular U.S. lottery jackpots is roughly 1 in 135,000,000. If you sell your quarter-million dollar house and use all the money to buy lottery tickets, your chance of winning is still only 1 in 540. If you play every day of the month (selling a house each day), your chance of winning the jackpot is still less than 1 in 15.

Of course, nothing in the previous paragraph applies to me. I don't buy lottery tickets, but I often win things. My winning streak started a few years ago. I won some expensive Java software at the end of an online seminar. Later that month, I won a microchip-enabled pinky ring (a memento from a 1998 Java conference). The following year I won a wireless PDA. Just last week, I won a fancy business-class printer.
