Next I define another enumeration.

```
enum shipCost {FIGHTER_COST = 25, BOMBER_COST, CRUISER_COST = 50};
```

This line of code defines the enumeration shipCost, which represents the cost in Resource Points for three kinds of ships in a strategy game. In it, I assign specific integer values to some of the enumerators. The numbers represent the Resource Point value of each ship. You can assign values to the enumerators if you want. Any enumerators that are not assigned values get the value of the previous enumerator plus one. Because I didn't assign a value to BOMBER_COST, it's initialized to 26.

Next I define a variable of this new enumeration type.

```
shipCost myShipCost = BOMBER_COST;
```

Then I demonstrate how you can use enumerators in arithmetic calculations.

```
(CRUISER_COST - myShipCost)
```

This piece of code calculates the cost of upgrading a Bomber to a Cruiser. The calculation is the same as 50 - 26, which evaluates to 24.

# INTRODUCING LOST FORTUNE

The final project for this chapter, Lost Fortune, is a personalized adventure game in which the player enters a few pieces of information, which the computer uses to enhance a basic adventure story. Figure 1.9 shows a sample run.

Instead of presenting all the code at once, I'll go through it one section at a time. You can download the code for this program from the Course Technology website (www.courseptr.com/downloads). The program is in the Chapter 1 folder; the filename is lost_fortune.cpp.

# Setting Up the Program

First I create some initial comments, include two necessary files, and write a few using directives.

```
// Lost Fortune
// A personalized adventure
```

```
#include <iostream>
#include <string>
```