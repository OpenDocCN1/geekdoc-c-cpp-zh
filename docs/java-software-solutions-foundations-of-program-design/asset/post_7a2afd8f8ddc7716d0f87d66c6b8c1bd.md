
![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_623_0.png)

*FIGURE 12.5 The Towers of Hanoi puzzle*

## The Towers of Hanoi

The Towers of Hanoi puzzle was invented in the 1880s by Edouard Lucas, a French mathematician. It has become a favorite among computer scientists, because its solution is an excellent demonstration of recursive elegance.

The puzzle consists of three upright pegs and a set of disks with holes in the middle so that they slide onto the pegs. Each disk has a different diameter. Initially, all of the disks are stacked on one peg in order of size such that the largest disk is on the bottom, as shown in Figure 12.5.

The goal of the puzzle is to move all of the disks from their original (first) peg to the destination (third) peg. We can use the "extra" peg as a temporary place to put disks, but we must obey the following three rules:

- We can move only one disk at a time.
- We cannot place a larger disk on top of a smaller disk.
- All disks must be on some peg except for the disk in transit between pegs.

These rules imply that we must move smaller disks "out of the way" in order to move a larger disk from one peg to another. Figure 12.6 shows the step-by-step solution for the Towers of Hanoi puzzle using three disks. In order to ultimately move all three disks from the first peg to the third peg, we first have to get to the point where the smaller two disks are out of the way on the second peg so that the largest disk can be moved from the first peg to the third peg.

The first three moves shown in Figure 12.6 can be thought of as moving the smaller disks out of the way. The fourth move puts the largest disk in its final place. The last three moves then put the smaller disks to their final place on top of the largest one.

Let's use this idea to form a general strategy. To move a stack of N disks from the original peg to the destination peg:

- Move the topmost N-1 disks from the original peg to the extra peg.
- Move the largest disk from the original peg to the destination peg.
- Move the N-1 disks from the extra peg to the destination peg.

*FIGURE 12.6 A solution to the three-disk Towers of Hanoi puzzle*

This strategy lends itself nicely to a recursive solution. The step to move the N-1 disks out of the way is the same problem all over again: moving a stack of disks. For this subtask, though, there is one less disk, and our destination peg is what we were originally calling the extra peg. An analogous situation occurs after we've moved the largest disk and we have to move the original N-1 disks again.

The base case for this problem occurs when we want to move a "stack" that consists of only one disk. That step can be accomplished directly and without recursion.

The program in Listing 12.3 creates a TowersOfHanoi object and invokes its solve method. The output is a step-by-step list of instructions that describe how the disks should be moved to solve the puzzle. This example uses four disks, which is specified by a parameter to the TowersOfHanoi constructor.

The TowersOfHanoi class shown in Listing 12.4 uses the solve method to make an initial call to moveTower, the recursive method. The initial call indicates that all of the disks should be moved from peg 1 to peg 3, using peg 2 as the extra position.

The moveTower method first considers the base case (a "stack" of one disk). When that occurs, it calls the moveOneDisk method that prints a single line

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_624_0.png)

VideoNote Exploring the Towers of Hanoi.

### LISTING 12.3

```java
//****************************************************************
// SolveTowers.java      Author: Lewis/Loftus
//
// Demonstrates recursion.
//****************************************************************

public class SolveTowers
{
    //-------------------------------------------------------------
    // Creates a TowersOfHanoi puzzle and solves it.
    //-------------------------------------------------------------
    public static void main (String[] args)
    {
        TowersOfHanoi towers = new TowersOfHanoi (4);

        towers.solve();
    }
}
```

### OUTPUT

```text
Move one disk from 1 to 2
Move one disk from 1 to 3
Move one disk from 2 to 3
Move one disk from 1 to 2
Move one disk from 3 to 1
Move one disk from 3 to 2
Move one disk from 1 to 2
Move one disk from 1 to 3
Move one disk from 2 to 3
Move one disk from 2 to 1
Move one disk from 3 to 1
Move one disk from 2 to 3
Move one disk from 1 to 2
Move one disk from 1 to 3
Move one disk from 2 to 3
```

describing that particular move. If the stack contains more than one disk, we call moveTower again to get the N-1 disks out of the way, then move the largest disk, then move the N-1 disks to their final destination with yet another call to moveTower.

### LISTING 12.4

```java
//***************************************************************************
// TowersOfHanoi.java      Author: Lewis/Loftus
//
// Represents the classic Towers of Hanoi puzzle.
//***************************************************************************

public class TowersOfHanoi
{
    private int totalDisks;

    //-----------------------------------------------
    // Sets up the puzzle with the specified number of disks.
    //-----------------------------------------------
    public TowersOfHanoi (int disks)
    {
        totalDisks = disks;
    }

    //-----------------------------------------------
    // Performs the initial call to moveTower to solve the puzzle.
    // Moves the disks from tower 1 to tower 3 using tower 2.
    //-----------------------------------------------
    public void solve ()
    {
        moveTower (totalDisks, 1, 3, 2);
    }

    //-----------------------------------------------
    // Moves the specified number of disks from one tower to another
    // by moving a subtower of n-1 disks out of the way, moving one
    // disk, then moving the subtower back. Base case of 1 disk.
    //-----------------------------------------------
    private void moveTower (int numDisks, int start, int end, int temp)
    {
        if (numDisks == 1)
            moveOneDisk (start, end);
        else
        {
            moveTower (numDisks-1, start, temp, end);
            moveOneDisk (start, end);
            moveTower (numDisks-1, temp, end, start);
        }
    }

    //------------------------------------------------------------
    // Prints instructions to move one disk from the specified start
    // tower to the specified end tower.
    //------------------------------------------------------------
    private void moveOneDisk (int start, int end)
    {
        System.out.println ("Move one disk from " + start + " to " +
            end);
    }
}
```

Note that the parameters to moveTower describing the pegs are switched around as needed to move the partial stacks. This code follows our general strategy and uses the moveTower method to move all partial stacks. Trace the code carefully for a stack of three disks to understand the processing. Compare the processing steps to Figure 12.6.

### KEY CONCEPT

The Towers of Hanoi solution has exponential complexity, which is very inefficient. Yet the implementation of the solution is incredibly short and elegant.

Contrary to its short and elegant implementation, the solution to the Towers of Hanoi puzzle is terribly inefficient. To solve the puzzle with a stack of N disks, we have to make 2^N-1 individual disk moves. This situation is an example of exponential complexity. As the number of disks increases, the number of required moves increases exponentially.

Legend has it that priests of Brahma are working on this puzzle in a temple at the center of the world. They are using 64 gold disks, moving them between pegs of pure diamond. The downside is that when the priests finish the puzzle, the world will end. The upside is that even if they move one disk every second of every day, it will take them over 584 billion years to complete it. That's with a puzzle of only 64 disks! It is certainly an indication of just how intractable exponential algorithmic complexity is.

### SELF-REVIEW QUESTIONS (see answers in Appendix N)

- SR 12.11 Under what conditions does the recursion stop in the MazeSearch program?
- SR 12.12 Identify where in the MazeSearch program each of the following is provided.
