# Traversing a Maze

Solving a maze involves a great deal of trial and error: following a path, backtracking when you cannot go farther, and trying other untried options. Such activities often are handled nicely using recursion. The program shown in Listing 12.1 creates a Maze object and attempts to traverse it.

# LISTING 12.1

```
//****************************************************************
// MazeSearch.java      Author: Lewis/Lofthus
//
// Demonstrates recursion.
//****************************************************************
public class MazeSearch
{
    //-------------------------------------------------------------
    // Creates a new maze, prints its original form, attempts to
    // solve it, and prints out its final form.
    //-------------------------------------------------------------
    public static void main (String[] args)
    {
        Maze labyrinth = new Maze();

        System.out.println (labyrinth);

        if (labyrinth.traverse (0, 0))
            System.out.println ("The maze was successfully traversed!");
        else
            System.out.println ("There is no possible path.");

        System.out.println (labyrinth);
    }
}
```

# OUTPUT

1110110001111
1011101111001
0000101010100
1110111010111
101000111001
1011111101111
1000000000000
1111111111111