
axis (see Figure 7.7). The distance and angle together constitute polar coordinates. You can define a second structure to represent this view of a position:

```
struct polar
{
    double distance; // distance from origin
    double angle;    // direction from origin
};
```

![](img/cd111a87c1db9aff4db4b18834327463_361_0.png)

Figure 7.7 Polar coordinates.

Let's construct a function that displays the contents of a type polar structure. The math functions in the C++ library (borrowed from C) assume that angles are in radians, so you need to measure angles in units. But for display purposes, you can convert radian measure to degrees. This means multiplying by 180/π, which is approximately 57.29577951. Here's the function:

```
// show polar coordinates, converting angle to degrees
void show_polar(polar dapos)
{
    using namespace std;
    const double Rad_to_deg = 57.29577951;

    cout << "distance = " << dapos.distance << "\n";
    cout << "angle = " << dapos.angle * Rad_to_deg;
    cout << " degrees\n";
}
```

## Chapter 7 Functions: C++'s Programming Modules

Notice that the formal variable is type polar. When you pass a polar structure to this function, the structure contents are copied into the data structure, and the function then uses that in its work. Because data is a structure, the function uses the membership (dot) operator (see Chapter 4) to identify structure members.

Next, let's try something ambitious and write a function that converts rectangular coordinates to polar. We'll have the function accept a rect structure as its argument and return a polar structure to the calling function. This function includes functions from the math library, so the program has to include the cmath header file (math.h on older systems). Also on some systems you have to tell the compiler to load the math library (see Chapter 1, "Getting Started with C++"). You can use the Pythagorean theorem to get the distance from the horizontal and vertical vertices:

```
distance = sqrt( x * x + y * y)
```

The atan2() function from the math library calculates the angle from the x and y values:

(There's also an atan() function, but it doesn't distinguish between 180 degrees apart. That uncertainty is no more desirable in a math function than it is in a wilderness guide.)

Given these formulas, you can write the function as follows:

```
// convert rectangular to polar coordinates
polar rect_to_polar(rect xypos) // returns type polar
{
    polar answer;

    answer.distance =
    sqrt(xypos.x * xypos.x + xypos.y * xypos.y);
    answer.angle = atan2(xypos.y, xypos.x);
    return answer; // returns a polar structure
}
```

Now that the functions are ready, writing the rest of the program is straightforward. Listing 7.12 presents the:

## Listing 7.12 structfun.cpp

```
// structfun.cpp -- functions with a structure stream
#include <iostream>
#include <cmath>

// structure declarations
struct polar
{
    double distance; // distance from origin
    double angle; // direction from origin
};

struct rect
{
    double x;      // horizontal distance from origin
    double y;      // vertical distance from origin
}

// prototypes
polar rect_to_polar(rect xypos);
void show_polar(polar dapos);

int main()
{
    using namespace std;
    rect rplace;
    polar pplace;

    cout << "Enter the x and y values: ";
    while (cin >> rplace.x >> rplace.y) // slick use of cin
    {
        pplace = rect_to_polar(rplace);
        show_polar(pplace);
        cout << "Next two numbers (q to quit): ";
    }
    cout << "Done.\n";
    return 0;
}

// convert rectangular to polar coordinates
polar rect_to_polar(rect xypos)
{
    using namespace std;
    polar answer;

    answer.distance = sqrt(xypos.x * xypos.x + xypos.y * xypos.y);
    answer.angle = atan2(xypos.y, xypos.x); // returns a polar structure
    return answer;
}

// show polar coordinates, converting angle to degrees
void show_polar(polar dapos)
{
    using namespace std;
    const double Rad_to_deg = 57.29577951;

    cout << "distance = " << dapos.distance << ",";
    cout << " angle = " << dapos.angle * Rad_to_deg << ",";
    cout << " degrees\n";
}
```

## Chapter 7 Functions: C++'s Programming Modules

Note
Some compilers require explicit instructions to search the math library. For example, older versions of g++ use this command line:

```
g++ structfun.C -lm
```

Here is a sample run of the program in Listing 7.12:

```
Enter the x and y values: 30 40
distance = 50, angle = 53.1301 degrees
Next two numbers (q to quit): -100 100
distance = 141.421, angle = 135 degrees
Next two numbers (q to quit): q
```

### Program Notes

We've already discussed the two functions in Listing 7.12, so let's review how the program uses cin to control a loop:

Recall that cin is an object of the istream class. The extraction operator (>>) is designed in such a way that cin >> rplace.x is also an object of that type. As you'll see in Chapter 11, "Working with Classes," class operators are implemented with functions.
What happens when you use cin >> rplace.x is that the program calls a function that returns a type stream value. If you apply the extraction operator to the cin >> rplace.x object (as in cin >> rplace.x >> rplace.y), you again get an object of the istream class. Thus, the entire while loop test expression evaluates to cin, which, as you may recall, when used in the context of a test expression, is converted to a boolean value of true or false, depending on whether input succeeded. In the loop Listing 7.12, for example, cin expects to enter two numbers. If the user enters q, as shown in the sample output, cin recognizes that q is not a number. It leaves the q in the input queue and returns a value that's converted to false, terminating the loop.

Compare that approach for reading numbers to this one:

To terminate this loop early, you enter a negative number. This restricts input to non-negative values. This restriction fits the needs of some programs, but more typically you would want a means of terminating a loop that doesn't exclude certain numeric values. Using cin >> as the test condition eliminates such restrictions because it accepts all valid numeric input. You should keep this in mind when you need an input for numbers. Also, you should keep in mind that non-numeric input sets an error condition that prevents the reading of any more input. If a program inputs up to the input loop, you must use cin.clear() to reset input, and you might then need to get rid of the offending input by reading it. Listing 7.7 illustrates these techniques.

### Functions and Structures

would we want a means of terminating a loop that doesn't exclude certain numeric values. Using cin >> as the test condition eliminates such restrictions because it accepts all valid numeric input. You should keep this in mind when you need an input for numbers. Also, you should keep in mind that non-numeric input sets an error condition that prevents the reading of any more input. If a program inputs up to the input loop, you must use cin.clear() to reset input, and you might then need to get rid of the offending input by reading it. Listing 7.7 illustrates these techniques.

### Passing Structure Addresses

Suppose you want to save time and space by passing the address of a structure instead of passing the entire structure. This requires rewriting the functions so they use pointers to structures. First, let's look at how you rewrite the show_polar() function. You need to make three changes:

- When calling the function, pass the address of the structure (&polar) rather than the structure itself (pplace).
- Declare the formal parameter to be a pointer-to-polar—that is, type *. Because the function shouldn't modify the structure, use the const modifier.
- Because the formal parameter is a pointer instead of a structure, use the indirect membership operator (->) rather than the membership operator (dot).

After these changes are made, the function looks like this:

```
// show polar coordinates, converting angle to degrees
void show_polar(const polar * pda) {
    using namespace std;
    const double Rad_to_deg = 57.29577951;

    cout << "distance = " << pda->distance << "\n";
    cout << "angle = " << pda->angle * Rad_to_deg << "\n";
    cout << "degrees\n";
}
```

Next, let's alter rect_to_polar. This is more involved because the original rect_to_polar function returns a structure. To take full advantage of pointer efficiency, you should use a pointer instead of a return value. The way to do this is to pass two pointers to the function. The first points to the structure to be converted, and the second points to the structure that is to hold the conversion. Instead of returning a new structure, the function modifies an existing structure in the calling function. Hence, the first argument is const pointer, the second is not const. Otherwise, you apply the same principles to convert show_polar() to pointer arguments. Listing 7.13 shows the reworked program.
