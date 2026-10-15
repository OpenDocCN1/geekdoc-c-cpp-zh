
In fact, the increment portion of the for loop can perform any calculation, not just a simple increment or decrement. Consider the program shown in Listing 6.3, which prints multiples of a particular value up to a particular limit.

The increment portion of the for loop in the Multiples program adds the value entered by the user after each iteration. The number of values printed per line is controlled by counting the values printed and then moving to the next line whenever count is evenly divisible by the PER_LINE constant.

## LISTING 6.3

```
//****************************************************************
// Multiples.java      Author: Lewis/Loftus
//
// Demonstrates the use of a for loop.
//****************************************************************

import java.util.Scanner;

public class Multiples
{
    //-------------------------------------------------------------
    // Prints multiples of a user-specified number up to a user-
    // specified limit.
    //-------------------------------------------------------------
    public static void main (String[] args)
    {
        final int PER_LINE = 5;
        int value, limit, mult, count = 0;

        Scanner scan = new Scanner (System.in);

        System.out.print ("Enter a positive value: ");
        value = scan.nextInt();

        System.out.print ("Enter an upper limit: ");
        limit = scan.nextInt();

        System.out.println ();
        System.out.println ("The multiples of " + value + " between " +
                            value + " and " + limit + " (inclusive) are:");

        for (mult = value; mult <= limit; mult += value)
        {
            System.out.print (mult + "\t");
```

## LISTING 6.3 continued

```
// Print a specific number of values per line of output
count++;
if (count % PER_LINE == 0)
    System.out.println();
}
}
```

## OUTPUT

Enter a positive value: 7
Enter an upper limit: 400

The multiples of 7 between 7 and 400 (inclusive) are:
7    14    21    28    35
42    49    56    63    70
77    84    91    98    105
112    119    126    133    140
147    154    161    168    175
182    189    196    203    210
217    224    231    238    245
252    259    266    273    280
287    294    301    308    315
322    329    336    343    350
357    364    371    378    385
392    399

The Stars program in Listing 6.4 shows the use of nested for loops. The output is a triangle shape made of asterisk characters. The outer loop executes exactly 10 times. Each iteration of the outer loop prints one line of the output. The inner loop performs a different number of iterations depending on the line value controlled by the outer loop. Each iteration of the inner loop prints one star on the current line. Writing programs that print variations on this triangle configuration are included in the programming projects at the end of the chapter.

## The for-each Loop

A variation of the for statement, often called the for-each loop, is particularly helpful in situations that involve iterators. In Chapter 5 we discussed that some

## LISTING 6.4

```
//***************************************************************************
// Stars.java      Author: Lewis/Loftus
//
// Demonstrates the use of nested for loops.
//***************************************************************************

public class Stars
{
    //-------------------------------------------------------------
    // Prints a triangle shape using asterisk (star) characters.
    //-------------------------------------------------------------
    public static void main (String[] args)
    {
        final int MAX_ROWS = 10;

        for (int row = 1; row <= MAX_ROWS; row++)
        {
            for (int star = 1; star <= row; star++)
                System.out.print ("*");

            System.out.println();
        }
    }
}
```

## OUTPUT

```
*
**
***
****
*****
******
*******
********
*********
**********
```

objects are considered to be iterators, which have hasNext and next methods to process each item from a group. If an object has implemented the Iterable interface, then we can use a variation of the for loop to process items using a simplified syntax.

KEY CONCEPT
The for-each version of a for loop simplifies the processing of all elements in an Iterable object.

An ArrayList object is an Iterable object. Therefore, for example, if library is an ArrayList<Book> object (that is, an ArrayList that manages Book objects), we can use a for loop to process each Book object in the collection as follows:

```
for (Book myBook : library)
    System.out.println (myBook);
```

This code can be read as follows: for each Book in library, print the book object. The variable myBook takes the value of each Book object in the collection in turn, and the body of the loop can process it appropriately. That succinct for-each loop is essentially equivalent to the following:

```
Book myBook;
while (bookList.hasNext())
{
    myBook = bookList.next();
    System.out.println (myBook);
}
```

This version of the for loop can also be used on arrays, which are discussed in Chapter 8. We use the for-each loop as appropriate in various situations throughout the rest of the book.

## Comparing Loops

The three basic loop statements (while, do, and for) are functionally equivalent. Any particular loop written using one type of loop can be written using either of the other two loop types. Which type of loop we use depends on the situation.

As we mentioned earlier, the primary difference between a while loop and a do loop is when the condition is evaluated. If we know we want to execute the loop body at least once, a do loop is usually the better choice. The body of a while loop, on the other hand, might not be executed at all if the condition is initially false. Therefore, we say that the body of a while loop is executed zero or more times, but the body of a do loop is executed one or more times.

KEY CONCEPT
The loop statements are functionally equivalent. Which one you use should depend on the situation.

A for loop is like a while loop in that the condition is evaluated before the loop body is executed. We generally use a for loop when the number of times we want to iterate through a loop is fixed or can be easily calculated. In many situations, it is simply more convenient to separate the code that sets up and controls the loop iterations inside the for loop header from the body of the loop.

## SELF-REVIEW QUESTIONS (see answers in Appendix N)

SR 6.12 When would we use a for loop instead of a while loop?

SR 6.13 What output is produced by the following code fragment?

```
int value = 0;
for (int num = 10; num <= 40; num += 10)
{
    value = value + num;
}
System.out.println (value);
```

SR 6.14 What output is produced by the following code fragment?

```
int value = 0;
for (int num = 10; num < 40; num += 10)
{
    value = value + num;
}
System.out.println (value);
```

SR 6.15 What output is produced by the following code fragment?

```
int value = 6;
for (int num = 1; num <= value; num++)
{
    for (int i = 1; i <= (value - num); i++)
        System.out.print (" ");
    for (int i = 1; i <= ((2 * num) - 1); i++)
        System.out.print ("*");
    System.out.println ();
}
```

SR 6.16 Assume die is a Die object (as defined in Section 4.2). Write a code fragment that will roll die 100 times and output the average value rolled.

## 6.5 Drawing with Loops and Conditionals

Conditionals and loops greatly enhance our ability to generate interesting graphics.

The Bullseye program shown in Listing 6.5 draws a target. The drawing actually occurs in the BullseyePanel class, shown in Listing 6.6. The paintComponent of the BullseyePanel class uses an if statement to alternate the colors between black and white.

Note that each ring is actually drawn as a filled circle (an oval of equal width and length). Because we draw the circles on top of each other, the inner circles

## LISTING 6.5

```
//************************************************************************
// Bullseye.java Author: Lewis/Loftus
//
// Demonstrates the use of loops to draw.
//************************************************************************

import javax.swing.JFrame;

public class Bullseye
{
    //------------------------------------------------------------
    // Creates the main frame of the program.
    //------------------------------------------------------------
    public static void main (String[] args)
    {
        JFrame frame = new JFrame ("Bullseye");
        frame.setDefaultCloseOperation (JFrame.EXIT_ON_CLOSE);

        BullseyePanel panel = new BullseyePanel();

        frame.getContentPane().add(panel);
        frame.pack();
        frame.setVisible(true);
    }
}
```

## DISPLAY

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_313_0.png)
