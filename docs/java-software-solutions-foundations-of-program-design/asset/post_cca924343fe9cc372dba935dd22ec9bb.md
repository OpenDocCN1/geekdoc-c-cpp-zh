
## LISTING 12.7 continued

```
// intermediate points are computed, and each line segment is
// drawn as a fractal.
//-------------------------------------------------------------
public void drawFractal (int order, int x1, int y1, int x5, int y5,
    Graphics page)
{
    int deltaX, deltaY, x2, y2, x3, y3, x4, y4;

    if (order == 1)
        page.drawLine (x1, y1, x5, y5);
    else
    {
        deltaX = x5 - x1; // distance between end points
        deltaY = y5 - y1;

        x2 = x1 + deltaX / 3; // one third
        y2 = y1 + deltaY / 3;

        x3 = (int) ((x1+x5)/2 + SQ * (y1-y5)); // tip of projection
        y3 = (int) ((y1+y5)/2 + SQ * (x5-x1));

        x4 = x1 + deltaX * 2/3; // two thirds
        y4 = y1 + deltaY * 2/3;

        drawFractal (order-1, x1, y1, x2, y2, page);
        drawFractal (order-1, x2, y2, x3, y3, page);
        drawFractal (order-1, x3, y3, x4, y4, page);
        drawFractal (order-1, x4, y4, x5, y5, page);
    }
}

//-------------------------------------------------------------
// Performs the initial calls to the drawFractal method.
//-------------------------------------------------------------
public void paintComponent (Graphics page)
{
    super.paintComponent (page);

    page.setColor (Color.green);

    drawFractal (current, TOPX, TOPY, LEFTX, LEFTY, page);
    drawFractal (current, LEFTX, LEFTY, RIGHTX, RIGHTY, page);
    drawFractal (current, RIGHTX, RIGHTY, TOPX, TOPY, page);
}
```

## LISTING 12.7 continued

```
//----------------------------------------------------------------
// Sets the fractal order to the value specified.
//----------------------------------------------------------------
public void setOrder (int order)
{
    current = order;
}

//----------------------------------------------------------------
// Returns the current order.
//----------------------------------------------------------------
public int getOrder ()
{
    return current;
}
}
```

The variable current represents the order of the fractal to be drawn. Each recursive call to drawFractal decrements the order by 1. The base case of the recursion occurs when the order of the fractal is 1, which results in a simple line segment between the coordinates specified by the parameters.

If the order of the fractal is higher than 1, three additional points are computed. In conjunction with the parameters, these points form the four line segments of the modified fractal. Figure 12.8 shows the transformation.

Based on the position of the two end points of the original line segment, a point one-third of the way and a point two-thirds of the way between them are computed. The calculation of <x₃, y₃>, the point at the tip of the protrusion, is more convoluted and uses a simplifying constant that incorporates multiple geometric relationships. The calculations to determine the three new points actually have nothing to do with the recursive technique used to draw the fractal, and so we won’t discuss the details of these computations here.

An interesting mathematical feature of a Koch snowflake is that it has an infinite perimeter but a finite area. As the order of the fractal increases, the perimeter grows exponentially larger, with a mathematical limit of infinity. However, a rectangle large enough to surround the second-order fractal for the Koch snowflake is large enough to contain all higher-order fractals. The shape is restricted forever in area, but its perimeter gets infinitely longer.

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_638_0.png)

FIGURE 12.8 The transformation of each line segment of a Koch snowflake

## SELF-REVIEW QUESTIONS (see answers in Appendix N)

- SR 12.16 What is the base case for the TiledPictures program?
- SR 12.17 What is a fractal? What does it have to do with recursion?

## Summary of Key Concepts

- Recursion is a programming technique in which a method calls itself. A key to being able to program recursively is to be able to think recursively.
- Any recursive definition must have a non-recursive part, called the base case, which permits the recursion to eventually end.
- Mathematical problems and formulas are often expressed recursively.
- Each recursive call to a method creates new local variables and parameters.
- A careful trace of recursive processing can provide insight into the way it is used to solve a problem.
- Recursion is the most elegant and appropriate way to solve some problems, but for others it is less intuitive than an iterative solution.
- The Towers of Hanoi solution has exponential complexity, which is very inefficient. Yet the implementation of the solution is incredibly short and elegant.
- A fractal is a geometric shape that is defined naturally in a recursive manner.

## Exercises

Visit www.myprogramminglab.com to complete many of these Exercises online and get instant feedback.

- EX 12.1 Write a recursive definition of a valid Java identifier (see Chapter 1).
- EX 12.2 Write a recursive definition of x^y (x raised to the power y), where x and y are integers and y > 0.
- EX 12.3 Write a recursive definition of i * j (integer multiplication), where i > 0. Define the multiplication process in terms of integer addition. For example, 4 * 7 is equal to 7 added to itself 4 times.
- EX 12.4 Write a recursive definition of the Fibonacci numbers. The Fibonacci numbers are a sequence of integers, each of which is the sum of the previous two numbers. The first two numbers in the sequence are 0 and 1. Explain why you would not normally use recursion to solve this problem.

EX 12.5 Modify the method that calculates the sum of the integers between 1 and N shown in this chapter. Have the new version match the following recursive definition: The sum of 1 to N is the sum of 1 to (N/2) plus the sum of (N/2 + 1) to N. Trace your solution using an N of 7.

EX 12.6 Write a recursive method that returns the value of N! (N factorial) using the definition given in this chapter. Explain why you would not normally use recursion to solve this problem.

EX 12.7 Write a recursive method to reverse a string. Explain why you would not normally use recursion to solve this problem.

EX 12.8 Design or generate a new maze for the MazeSearch program in this chapter and rerun the program. Explain the processing in terms of your new maze, giving examples of a path that was tried but failed, a path that was never tried, and the ultimate solution.

EX 12.9 Annotate the lines of output of the SolveTowers program in this chapter to show the recursive steps.

EX 12.10 Produce a chart showing the number of moves required to solve the Towers of Hanoi puzzle using the following number of disks: 2, 3, 4, 5, 6, 7, 8, 9, 10, 15, 20, and 25.

EX 12.11 How many line segments are used to construct a Koch snowflake of order N? Produce a chart showing the number of line segments that make up a Koch snowflake for orders 1 through 9.

## Programming Projects

Visit www.myprogramminglab.com to complete many of these Programming Projects online and get instant feedback.

PP 12.1 Design and implement a recursive version of the PalindromeTester program from Chapter 5.

PP 12.2 Design and implement a program that implements Euclid’s algorithm for finding the greatest common divisor of two positive integers. The greatest common divisor is the largest integer that divides both values without producing a

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_640_0.png)

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_640_1.png)

VideoNote
Developing a solution of PP 12.1.

remainder. An iterative version of this method was part of the RationalNumber class presented in Chapter 7. In a class called DivisorCalc, define a static method called gcd that accepts two integers, num1 and num2. Create a driver to test your implementation. The recursive algorithm is defined as follows:

- gcd (num1, num2) is num2 if num2 <= num1 and num2 divides num1
- gcd (num1, num2) is gcd (num2, num1) if num1 < num2
- gcd (num1, num2) is gcd (num2, num1%num2) otherwise

PP 12.3 Modify the Maze class so that it prints out the path of the final solution as it is discovered without storing it.

PP 12.4 Design and implement a program that traverses a 3D maze.

PP 12.5 Modify the TiledPictures program so that the repeated images appear in the lower-right quadrant.

PP 12.6 Design and implement a recursive program that solves the Non-Attacking Queens problem. That is, write a program to determine how eight queens can be positioned on an eight-by-eight chessboard so that none of them are in the same row, column, or diagonal as any other queen. There are no other chess pieces on the board.

PP 12.7 In the language of an alien race, all words take the form of Blurbs. A Blurb is a Whoozit followed by one or more Whatzits. A Whoozit is the character ‘x’ followed by zero or more ‘y’s. A Whatzit is a ‘q’ followed by either a ‘z’ or a ‘d’, followed by a Whoozit. Design and implement a recursive program that generates random Blurbs in this alien language.

PP 12.8 Design and implement a recursive program to determine whether a string is a valid Blurb as defined in PP12.7.

PP 12.9 Design and implement a recursive program to determine and print the Nth line of Pascal’s Triangle, as shown below. Each interior value is the sum of the two values above it. Hint: use an array to store the values on each line.
