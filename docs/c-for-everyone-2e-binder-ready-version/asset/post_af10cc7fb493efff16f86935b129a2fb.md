
In addition, one must also supply a “copy constructor” for making safe copies, for example, when passing an object as a function argument. The destructor, assignment operator, and copy constructor are often called the “big 3” operations of memory management in C++. (See Horstmann & Budd, *Big C++*, 2nd Ed., Chapter 15, for details.)

![](img/6ec8c4bdbdda7d4ab1f2166b5332154c_452_0.png)

![](img/6ec8c4bdbdda7d4ab1f2166b5332154c_452_1.png)

## Formulate the public interface of a class in C++.

- A mutator member function changes the object on which it operates.
- An accessor member function does not change the object on which it operates. Use `const` with accessors.

## Choose data members to represent the state of an object.

![](img/6ec8c4bdbdda7d4ab1f2166b5332154c_454_0.png)

- An object holds data members that are accessed by member functions.
- Every object has its own set of data members.
- Private data members can only be accessed by member functions of the same class.

![](img/6ec8c4bdbdda7d4ab1f2166b5332154c_454_1.png)

## Implement member functions of a class.

- Use the `ClassName::` prefix when defining member functions.
- The implicit parameter is a reference to the object on which a member function is applied.
- Explicit parameters of a member function are listed in the function definition.
- When calling another member function on the same object, do not use the dot notation.

## Design and implement constructors.

![](img/6ec8c4bdbdda7d4ab1f2166b5332154c_454_2.png)

- A constructor is called automatically whenever an object is created.
- The name of a constructor is the same as the class name.
- A default constructor has no arguments.
- A class can have multiple constructors.
- The compiler picks the constructor that matches the construction arguments.
- Be sure to initialize all number and pointer data members in a constructor.

## Use the technique of object tracing for visualizing object behavior.

- Write the member functions on the front of a card, and the data member values on the back.
- Update the values of the data members when a mutator member function is called.

## Discover classes that are needed for solving a programming problem.

![](img/6ec8c4bdbdda7d4ab1f2166b5332154c_454_3.png)

- To discover classes, look for nouns in the problem description.
- Concepts from the problem domain are good candidates for classes.
- A class aggregates another if its objects contain objects of the other class.
- Avoid parallel vectors by changing them into vectors of objects.

![](img/6ec8c4bdbdda7d4ab1f2166b5332154c_454_4.png)

- **R9.7** What is a member function, and how does it differ from a nonmember function?

- **R9.8** What is a mutator function? What is an accessor function?

- **R9.9** What happens if you forget the const in an accessor function? What happens if you accidentally supply a const in a mutator function?

- **R9.10** What is an implicit parameter? How does it differ from an explicit parameter?

- **R9.11** How many implicit parameters can a member function have? How many implicit parameters can a nonmember function have? How many explicit parameters can a function have?

- **R9.12** What is a constructor?

- **R9.13** What is a default constructor? What is the consequence if a class does not have a default constructor?

- **R9.14** How many constructors can a class have? Can you have a class with no constructors? If a class has more than one constructor, which of them gets called?

- **R9.15** What is encapsulation? Why is it useful?

- **R9.16** Data members are hidden in the private section of a class, but they aren't hidden very well at all. Anyone can read the private section. Explain to what extent the private reserved word hides the private members of a class.

- **R9.17** You can read the item_count data member of the CashRegister class with the get_count accessor function. Should there be a set_count mutator function to change it? Explain why or why not.

- **R9.18** Suppose you implement a ChessBoard class. Provide data members to store the pieces on the board and the player who has the next turn.

- **R9.19** In a nonmember function, it is easy to differentiate between calls to member functions and calls to nonmember functions. How do you tell them apart? Why is it not as easy for functions that are called from a member function?

- **R9.20** Using the object tracing technique described in Section 9.6, trace the program at the end of Section 9.4.

- **R9.21** Using the object tracing technique described in Section 9.6, trace the program in Worked Example 9.1.

- **R9.22** Design a modification of the BankAccount class in Worked Example 9.1 in which the first five transactions per month are free and a $1 fee is charged for every additional transaction. Provide a member function that deducts the fee at the end of a month. What additional data members do you need? Using the object tracing technique described in Section 9.6, trace a scenario that shows how the fees are computed over two months.

- **R9.23** Consider the following problem description:

  > Users place coins in a vending machine and select a product by pushing a button. If the inserted coins are sufficient to cover the purchase price of the product, the product is dispensed and change is given. Otherwise, the inserted coins are returned to the user.

  What classes should you use to implement it?

```cpp
private:
    . . .
};
```

## Engineering P9.24

Implement a class `Car` with the following properties. A car has a certain fuel efficiency (measured in miles/gallon) and a certain amount of fuel in the gas tank. The efficiency is specified in the constructor, and the initial fuel level is 0. Supply a member function `drive` that simulates driving the car for a certain distance, reducing the fuel level in the gas tank, and member functions `get_gas_level`, to return the current fuel level, and `add_gas`, to tank up. Sample usage:

```cpp
Car my_hybrid(50); // 50 miles per gallon
my_hybrid.add_gas(20); // Tank 20 gallons
my_hybrid.drive(100); // Drive 100 miles
cout << my_hybrid.get_gas_level() << endl; // Print fuel remaining
```

## Engineering P9.25

Write a program that prints all real solutions to the quadratic equation
ax^2 + bx + c = 0. Read in a, b, c and use the quadratic formula. You may assume that
a ≠ 0. If the discriminant b^2 − 4ac is negative, display a message stating that there are
no real solutions.

Implement a class `QuadraticEquation` whose constructor receives the coefficients a, b, c of the quadratic equation. Supply member functions `get_solution1` and `get_solution2` that get the solutions, using the quadratic formula, or 0 if no solution exists. The `get_solution1` function should return the smaller of the two solutions.

Supply a function

```cpp
bool has_solutions() const
```

that returns false if the discriminant is negative.

## Engineering P9.26

Design a class `Cannonball` to model a cannonball that is fired into the air. A ball has

- An x- and a y-position.
- An x- and a y-velocity.

Supply the following member functions:

- A constructor with an x-position (the y-position is initially 0)
- A member function `move(double sec)` that moves the ball to the next position (First compute the distance traveled in sec seconds, using the current velocities, then update the x- and y-positions; then update the y-velocity by taking into account the gravitational acceleration of −9.81 m/sec^2; the x-velocity is unchanged.) (See Exercise P4.29 for additional details.)
- A member function `shoot` whose parameters are the angle α and initial velocity v (Compute the x-velocity as v cos α and the y-velocity as v sin α; then keep calling `move` with a time interval of 0.1 seconds until the y-position is ≤ 0; display the (x, y) position after every move.)

Use this class in a program that prompts the user for the starting angle and the initial velocity. Then call `shoot`.

## Engineering P9.27

The colored bands on the top-most resistor shown in the photo below indicate a resistance of 6.2 kΩ ±5%. The resistor tolerance of ±5% indicates the acceptable variation in the resistance. A 6.2 kΩ ±5% resistor could have a resistance as small as 5.89 kΩ or as large as 6.51 kΩ. We say that 6.2 kΩ is the nominal value of the resistance and that the actual value of the resistance can be any value between 5.89 kΩ and 6.51 kΩ.
