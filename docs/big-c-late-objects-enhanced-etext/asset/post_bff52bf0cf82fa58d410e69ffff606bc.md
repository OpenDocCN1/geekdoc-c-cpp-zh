
- **E9.7** Implement a class `StreetAddress`. An address has a house number, a street, an optional apartment number, a city, a state, and a postal code. Supply two constructors: one with an apartment number and one without. Supply a print member function that prints the address with the street (and optional apartment number) on one line and the city, state, and postal code on the next line. Supply a member function `comes_before` that tests whether one address comes before another when the addresses are compared by postal code.

- **E9.8** Implement a class `Student`. For the purpose of this exercise, a student has a name and a total quiz score. Supply an appropriate constructor and functions `get_name()`, `add_quiz(int score)`, `get_total_score()`, and `get_average_score()`. To compute the latter, you also need to store the number of quizzes that the student took.

- **E9.9** Modify the `Student` class of Exercise E9.8 to compute grade point averages. Member functions are needed to add a grade and get the current GPA. Specify grades as elements of a class `Grade`. Supply a constructor that constructs a grade from a string, such as `"B+"`. You will also need a function that translates grades into their numeric values (for example, `"B+"` becomes 3.3).

- **E9.10** Write a class `Bug` that models a bug moving along a horizontal line. The bug moves either to the right or left. Initially, the bug moves to the right, but it can turn to change its direction. In each move, its position changes by one unit in the current direction. Provide a constructor

    ```cpp
    Bug(int initial_position)
    ```

    and member functions

    ```cpp
    void turn()
    void move()
    int get_position()
    ```

    Sample usage:

    ```cpp
    Bug bugsy(10);
    bugsy.move(); // Now the position is 11
    bugsy.turn();
    bugsy.move(); // Now the position is 10
    ```

    Your main function should construct a bug, make it move and turn a few times, and print the actual and expected positions.

- **E9.11** Implement a class `Moth` that models a moth flying along the x-axis. The moth has a position, the distance from a fixed origin. When the moth moves toward a point of light, its new position is halfway between its old position and the position of the light source. Supply a constructor

    ```cpp
    Moth(double initial_position)
    ```

    and member functions

    ```cpp
    void move_to_light(double light_position)
    double get_position()
    ```

    Your main function should construct a moth, move it toward a couple of light sources, and check that the moth’s position is as expected.

- **E9.12** Implement classes `Person` and `StreetAddress`. Each person has a street address. Provide display functions in each class for displaying their contents. Distribute your code over three source files, one for each class, and one containing the main function. Construct two `Person` objects and display them.

![](img/d61019b035dd82beb581604273c0ee6b_521_0.png)

The `open` function attempts to open the lock. The lock opens if the user first turns it right to the first number in the combination, then left to the second, and then right to the third.

```
class ComboLock
{
public:
    ComboLock(int secret1, int secret2, int secret3);
    void reset();
    void turn_left(int ticks);
    void turn_right(int ticks);
    bool open() const;
private:
    ...
};
```

## Engineering P9.19

Implement a class `Car` with the following properties. A car has a certain fuel efficiency (measured in miles/gallon) and a certain amount of fuel in the gas tank. The efficiency is specified in the constructor, and the initial fuel level is 0. Supply a member function `drive` that simulates driving the car for a certain distance, reducing the fuel level in the gas tank, and member functions `get_gas_level`, to return the current fuel level, and `add_gas`, to tank up. Sample usage:

```
Car my_hybrid(50);  // 50 miles per gallon
my_hybrid.add_gas(20);  // Tank 20 gallons
my_hybrid.drive(100);  // Drive 100 miles
cout << my_hybrid.get_gas_level() << endl;  // Print fuel remaining
```

## Engineering P9.20

Write a program that prints all real solutions to the quadratic equation $ax^2 + bx + c = 0$. Read in $a$, $b$, $c$, and use the quadratic formula. You may assume that $a \ne 0$. If the discriminant $b^2 - 4ac$ is negative, display a message stating that there are no real solutions.

Implement a class `QuadraticEquation` whose constructor receives the coefficients $a$, $b$, $c$ of the quadratic equation. Supply member functions `get_solution1` and `get_solution2` that get the solutions, using the quadratic formula, or 0 if no solution exists. The `get_solution1` function should return the smaller of the two solutions.

Supply a function

```
bool has_solutions() const
```

that returns false if the discriminant is negative.

## Engineering P9.21

Design a class `Cannonball` to model a cannonball that is fired into the air. A ball has

- An $x$- and a $y$-position.
- An $x$- and a $y$-velocity.

Supply the following member functions:

- A constructor with an $x$-position (the $y$-position is initially 0)
- A member function `move(double sec)` that moves the ball to the next position (First compute the distance traveled in `sec` seconds, using the current velocities, then update the $x$- and $y$-positions; then update the $y$-velocity by taking into account the gravitational acceleration of $-9.81\ \mathrm{m/sec^2}$; the $x$-velocity is unchanged.) (See Exercise P4.23 for additional details.)
- A member function `shoot` whose parameters are the angle $\alpha$ and initial velocity $v$ (Compute the $x$-velocity as $v\cos\alpha$ and the $y$-velocity as $v\sin\alpha$; then keep calling `move` with a time interval of 0.1 seconds until the $y$-position is ≤ 0; display the ($x$, $y$) position after every move.)

Use this class in a program that prompts the user for the starting angle and the initial velocity. Then call `shoot`.

## Engineering P9.22

The colored bands on the top-most resistor shown in the photo below indicate a resistance of 6.2 kΩ ±5%. The resistor tolerance of ±5% indicates the acceptable variation in the resistance. A 6.2 kΩ ±5% resistor could have a resistance as small as 5.89 kΩ or as large as 6.51 kΩ. We say that 6.2 kΩ is the *nominal value* of the resistance and that the actual value of the resistance can be any value between 5.89 kΩ and 6.51 kΩ.

![](img/d61019b035dd82beb581604273c0ee6b_522_0.png)

Write a C++ program that represents a resistor as a class. Provide a single constructor that accepts values for the nominal resistance and tolerance and then determines the actual value randomly. The class should provide public member functions to get the nominal resistance, tolerance, and the actual resistance.

Write a main function for the C++ program that demonstrates that the class works properly by displaying actual resistances for ten 330 Ω ±10% resistors.

## Engineering P9.23

In the `Resistor` class from Exercise P9.22, supply a member function that returns a string consisting of the four colors of the “color bands” for the resistance and tolerance. A resistor has four color bands:

- The first band is the first significant digit of the resistance value.
- The second band is the second significant digit of the resistance value.
- The third band is the decimal multiplier.
- The fourth band indicates the tolerance.

![](img/d61019b035dd82beb581604273c0ee6b_522_1.png)

| Color | Digit | Multiplier | Tolerance |
|---|---:|---:|---:|
| Black | 0 | ×10⁰ | — |
| Brown | 1 | ×10¹ | ±1% |
| Red | 2 | ×10² | ±2% |
| Orange | 3 | ×10³ | — |
| Yellow | 4 | ×10⁴ | — |
| Green | 5 | ×10⁵ | ±0.5% |
