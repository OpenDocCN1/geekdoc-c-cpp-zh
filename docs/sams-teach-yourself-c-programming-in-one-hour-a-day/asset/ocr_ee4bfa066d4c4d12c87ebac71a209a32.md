# LESSON 11 Implementing Structures, Unions, and TypeDefs

FIGURE 11.1

| A type int variable (x) | mybox.topleft.x | A type coord structure (topleft) |
|---|---|---|
| A type int variable (y) | mybox.topleft.y | A type rectangle structure (mybox) |
| A type int variable (x) | mybox.bottomrt.x | A type coord structure (bottomrt) |
| A type int variable (y) | mybox.bottomrt.y |

The relationship between a structure, structures within a structure, and the structure members.

Listing 11.2 presents an example of using structures that contain other structures. This listing takes input for the coordinates of a rectangle and calculates and displays the rectangle's area. Note the program's assumptions, given in comments near the start of the program (lines 3 through 8).

# Input

# LISTING 11.2 struct c: A Demonstration of Structures that Contain Other Structures

```
/* Demonstrates structures that contain other structures. */
/* Receives input for corner coordinates of a rectangle and
calculates the area. Assumes that the y coordinate of the
lower-right corner is greater than the y coordinate of the
upper-left corner
```