
### R2.15
Modify the pseudocode for the program in How To 2.1 so that the program gives change in quarters, dimes, and nickels. You can assume that the price is a multiple of 5 cents. To develop your pseudocode, first work with a couple of specific values.

### R2.16
A cocktail shaker is composed of three cone sections. The volume of a cone section with height h and top and bottom radius r1 and r2 is V = π (r1² + r1 r2 + r2²) h / 3. Compute the total volume by hand for one set of realistic values for the radii and heights. Then develop an algorithm that works for arbitrary dimensions.

![](img/d61019b035dd82beb581604273c0ee6b_100_0.png)

### R2.17
You are cutting off a piece of pie like this, where c is the length of the straight part (called the chord length) and h is the height of the piece.

![](img/d61019b035dd82beb581604273c0ee6b_100_1.png)

There is an approximate formula for the area: A ≈ 2/3 c h + h³ / 2c. However, h is not so easy to measure, whereas the diameter d of a pie is usually well-known. Calculate the area where the diameter of the pie is 12 inches and the chord length of the segment is 10 inches. Generalize to an algorithm that yields the area for any diameter and chord length.

### R2.18
The following pseudocode describes how to obtain the name of a day, given the day number (0 = Sunday, 1 = Monday, and so on.) Define a string called names containing "SunMonTueWedThuFriSat". Compute the starting position as 3 x the day number. Extract the substring of names at the starting position with length 3. Check this pseudocode, using the day number 4. Draw a diagram of the string that is being computed, similar to Figure 4.

### R2.19
The following pseudocode describes how to swap two letters in a word. We are given a string str and two positions i and j. (i comes before j) Set first to the substring from the start of the string to the last position before i. Set middle to the substring from positions i + 1 to j - 1. Set last to the substring from position j + 1 to the end of the string. Concatenate the following five strings: first, the string containing just the character at position j, middle, the string containing just the character at position i, and last. Check this pseudocode, using the string "Gateway" and positions 2 and 4. Draw a diagram of the string that is being computed, similar to Figure 4.

### R2.20
Run the following program, and explain the output you get.

```cpp
#include <iostream>
using namespace std;

int main()
{
    int total;
    cout << "Please enter a number: ";
    double x1;
    cin >> x1;
    total = total + x1;
    cout << "total: " << total << endl;
    cout << "Please enter a number: ";
    double x2;
    cin >> x2;
    total = total + x2;
    cout << "total: " << total << endl;
    total = total / 2;
    cout << "total: " << total << endl;
    cout << "The average is " << total << endl;
    return 0;
}
```

Note the trace messages (in blue) that are inserted to show the current contents of the total variable. How do you fix the program? (The program has two separate errors.)

### R2.21
How do you get the first character of a string? The last character? How do you remove the first character? The last character?

### R2.22
For each of the following computations in C++, determine whether the result is exact, an overflow, or a roundoff error.

- a. 2.0 * 1.1
- b. 1.0E6 * 1.0E6
- c. 65536 * 65536
- d. 1000000 * 1000000

### R2.23
Write a program that prints the values

```
3 * 1000 * 1000 * 1000
3.0 * 1000 * 1000 * 1000
```

Explain the results.

### R2.24
This chapter contains a number of recommendations regarding variables and constants that make programs easier to read and maintain. Briefly summarize these recommendations.

## PRACTICE EXERCISES

### E2.1
Write a program that displays the dimensions of a letter-size (8.5 × 11 inches) sheet of paper in millimeters. There are 25.4 millimeters per inch. Use constants and comments in your program.

### E2.2
Write a program that computes and displays the circumference of a letter-size (8.5 × 11 inches) sheet of paper and the length of its diagonal

### E2.3
Write a program that reads a number and displays the square, cube, and fourth power. Use the `pow` function only for the fourth power.

### E2.4
Write a program that prompts the user for two integers and then prints

- The sum
- The difference
- The product
- The average

### E2.5
Write a program that prompts the user for two integers and then prints

- The distance (absolute value of the difference)
- The maximum (the larger of the two)
- The minimum (the smaller of the two)

Hint: The max and min functions are defined in the <algorithm> header.

### E2.6
Write a program that prompts the user for a measurement in meters and then converts it to miles, feet, and inches.

### E2.7
Write a program that prompts the user for a radius and then prints

- The area and circumference of a circle with that radius
- The volume and surface area of a sphere with that radius

### E2.8
Write a program that asks the user for the lengths of the sides of a rectangle and then prints

- The area and perimeter of the rectangle
- The length of the diagonal (use the Pythagorean theorem)

### E2.9
Improve the program discussed in How To 2.1 to allow input of quarters in addition to bills.

### E2.10
Write a program that asks the user to input

- The number of gallons of gas in the tank
- The fuel efficiency in miles per gallon
- The price of gas per gallon

Then print the cost per 100 miles and how far the car can go with the gas in the tank.

### E2.11
File names and extensions. Write a program that prompts the user for the drive letter (C:), the path (\Windows\System), the file name (Readme), and the extension (txt). Then print the complete file name C:\Windows\System\Readme.txt. (If you use UNIX or a Macintosh, skip the drive name and use / instead of \ to separate directories.)

### E2.12
Write a program that reads a number between 1,000 and 999,999 from the user and prints it with a comma separating the thousands. Here is a sample dialog; the user input is in color:

```
Please enter an integer between 1000 and 999999: 23456
23,456
```

(The \n character is explained in Special Topic 1.1.) Do the same for the letters E, L and O. Then write the message

```
H
E
E
L
L
O
```

in large letters.

### E2.18
Write a program that transforms numbers 1, 2, 3, ..., 12 into the corresponding month names January, February, March, ..., December. Hint: Make a very long string "January February March ...", in which you add spaces such that each month name has the same length. Then use substr to extract the month you want.

![](img/d61019b035dd82beb581604273c0ee6b_104_0.png)

© José Luis Gutiérrez/Stockphoto.

## PROGRAMMING PROJECTS

### P2.1
Easter Sunday is the first Sunday after the first full moon of spring. To compute the date, you can use this algorithm, invented by the mathematician Carl Friedrich Gauss in 1800:

- 1. Let y be the year (such as 1800 or 2001).
- 2. Divide y by 19 and call the remainder a. Ignore the quotient.
- 3. Divide y by 100 to get a quotient b and a remainder c.
- 4. Divide b by 4 to get a quotient d and a remainder e.
- 5. Divide 8 * b + 13 by 25 to get a quotient g. Ignore the remainder.
- 6. Divide 19 * a + b - d - g + 15 by 30 to get a remainder h. Ignore the quotient.
- 7. Divide c by 4 to get a quotient j and a remainder k.
- 8. Divide a + 11 * h by 319 to get a quotient m. Ignore the remainder.
- 9. Divide 2 * e + 2 * j - k - h + m + 32 by 7 to get a remainder r. Ignore the quotient.
- 10. Divide h - m + r + 90 by 25 to get a quotient n. Ignore the remainder.
- 11. Divide h - m + r + n + 19 by 32 to get a remainder p. Ignore the quotient.

Then Easter falls on day p of month n. For example, if y is 2001:

```
a = 6      g = 6      m = 0      n = 4
b = 20, c = 1    h = 18    r = 6    p = 15
d = 5, e = 0    j = 0, k = 1
```

Therefore, in 2001, Easter Sunday fell on April 15. Write a program that prompts the user for a year and prints out the month and day of Easter Sunday.

### P2.2
In this project, you will perform calculations with triangles. A triangle is defined by the x- and y-coordinates of its three corner points. Your job is to compute the following properties of a given triangle:

- the lengths of all sides
- the angles at all corners
- the perimeter
- the area
