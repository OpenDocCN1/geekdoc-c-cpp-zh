
Our main function calls three functions to implement the game. Each function has formal parameters of type player*. Since the player class uses the keyword virtual in its class declaration, the dynamic objects referenced by the formal parameters will call the overriding functions defined by the dynamic data type of the object, and the game will function properly for multiple players. We are now ready to convert to the pseudocode to C++ code:

```
/* * Program chapter10_9 -----------------------*/
/* Program chapter10_9 */
/* This program implements a version of the Iterated
Prisoner's Dilemma */
#include <iostream>
using namespace std;

#include "player.h" //base class player
#include "TitforTat.h" //TitforTat player

//Function prototypes
void setup(player*, player*);
void play_game(player*, player*);
void report(player*, player*);
int payoff(bool move, bool opponent_move);

int main()
{
// Declare objects.
player p1;
TitforTat p2;
player* ptr1 = &p1;
player* ptr2 = &p2;

// Notify players.
setup(ptr1, ptr2);
play_game(ptr1, ptr2);
cout << endl;
report(ptr1, ptr2);

return 0;
}
void setup(player* p1, player* p2)
{
// Announce players.
p1->print_name();
cout << " is playing ";
p2->print_algorithm();
cout << endl;
p2->print_name();
cout << " is playing ";
p2->print_algorithm();
cout << endl;
}

int payoff(bool move, bool opponent_move)
{
    if (move)
    {
        if (opponent_move)
        {
            return 3; // Both cooperate.
        }
        else
        {
            return 0; // I cooperate, opponent defects.
        }
    }
    else
    {
        if (opponent_move)
        {
            return 5; // I defect, opponent cooperates.
        }
        else
        {
            return 1; // Both defect.
        }
    }
}
/* Play a single game of the iterated
 * prisoner's dilemma between two players.
 */
void play_game(player* p1, player* p2)
{
    // Declare objects.
    int max_iterations;
    bool p1_move, p2_move, old_p1_move;
    cout << "Enter the number of iterations for the game: ";
    cin >> max_iterations;

    p1_move = p1->play(); // get the first move.
    p2_move = p2->play(); // get the first move.
    for (int i = 1; i < max_iterations; i++)
    {
        old_p1_move = p1_move;
        p1_move = p1->play(p2_move); // get the next move
        p2_move = p2->play(old_p1_move); // get the next move

        // Update the scores for this round of play.
        p1->accumulate(payoff(p1_move, p2_move));
        p2->accumulate(payoff(p2_move, p1_move));
    }
}

void report(player *p1, player *p2)
{
    if (p1->get_score() > p2->get_score()) // Player 1 won.
    {
        p1->print_name();
        cout << " (" << p1->get_score() << ") beat ";
        p2->print_name();
        cout << " (" << p2->get_score() << ").\n";
    }
    else if (p2->get_score() > p1->get_score()) // Player 2 won.
    {
        p2->print_name();
        cout << " (" << p2->get_score() << ") beat ";
        p1->print_name();
        cout << " (" << p1->get_score() << ").\n";
    }
    else // The players tied.
    {
        p1->print_name();
        cout << " and ";
        p2->print_name();
        cout << " tied at " << p1->get_score() << " each.\n";
    }
}
```

The class TitforTat is derived from the player class. The complete definition of the TitforTat class is

```
#ifndef TITFOR_TAT_H
#define TITFOR_TAT_H

#include "player.h"
//--------------------------------------------------------------*/
/*
 * This implements the Tit for Tat strategy.
 *
 * filename TitforTat.h
 */
class TitforTat : public player
{
public:
    // Print player's name.
    void print_name();

    // Print name of the player's algorithm.
    void print_algorithm();

    // Implement player's first move.
    bool play();

// Implements player's subsequent moves.
bool play(bool opponents_last_play);
};
#endif
```

```
/* This implements the Tit for Tat strategy with initial defect. */
#include <iostream>
using namespace std;
#include "TitforTat.h"
void TitforTat::print_name()
{
    cout << "Jeanine ";
}
// Print name of the player's algorithm.
void TitforTat::print_algorithm()
{
    cout << "Tit for Tat";
}
// Implement player's first move.
bool TitforTat::play()
{
    return false;
}
// Implements player's subsequent moves.
bool TitforTat::play(bool opponents_last_play)
{
    return opponents_last_play;
}
```

## 5. TESTING

A sample run of the program is as follows, with Jeanine playing the base class player:

Base Class Player is playing Always Cooperate.
Jeanine is playing Tit for Tat.
Enter the number of iterations for the game: 10
Jeanine (32) beat Base Class Player (27).

The difference in the score is the result of the first move, when player Jeanine defected and Base Class Player cooperated. On the remaining plays, both players cooperated.

## Modify!

Define a player class, derived from the base class, to implement an always-defect algorithm.

- 1. Run program chapter10_9 playing always defect against always cooperate. What are the results after 25 iterations?
- 2. Run program chapter10_9 playing always defect against tit for tat. What are the results after 25 iterations?
- 3. Remove the keyword virtual from the player class declaration. Run program chapter10_9. What is the output?

## SUMMARY

In C++ the class mechanism supports object-based programming. Classes are used to define new abstract data types, and overloading of operators allows these new data types to provide definitions for the existing, built in operators. Friend functions and overloading of operators provide for easy, convenient use of these new data types. The use of inheritance and virtual functions form the basis for object-oriented design of large programs. The utilization of these advanced topics are illustrated with the development of a Pixel class and the development of two new classes derived from the Rectangle class. The power of inheritance and virtual functions is demonstrated in a program to implement the iterated prisoner's dilemma.

## Key Terms

| base class | overloading operators |
| :--- | :--- |
| binary tree | pixel |
| derived class | polymorphism |
| dynamic binding | protected |
| generic programming | public inheritance |
| image processing | this pointer |
| inheritance | tree traversal |
| iterated prisoner's dilemma | virtual function |

## C++ Statement Summary

Prototype for member function of overloaded + operator:

```
return data type operator +(data type);
```

Example:

```
Pixel operator +(Pixel) const;
```

Prototype for friend function of overloaded + operator:

```
friend return data type operator +(data type, data type);
```

Example:

```
friend Pixel operator +(Pixel, Pixel);
```

### Prototype for friend function of overloaded << operator:

```
friend ostream& operator <<(ostream&, data type);
```

Example:

```
friend ostream& operator <<(ostream&, Pixel);
```

### Prototype for friend function of overloaded >> operator:

```
friend istream& operator >>(istream&, data type&);
```

Example:

```
friend istream& operator >>(istream&, Pixel&);
```

### Class definition for public inheritance

```
class classname : public base class name
```

Example:

```
class square : public rectangle
{
public:
...
protected:
...
};
```

### Specification of virtual functions

Prototype: virtual return data type function name (parameter list);

```
Example:
virtual void print(ostream&);
class Templates expression
template <typename identifier>
```

## Notes

- 1. Use constructors and member functions of the base class to assign values to inherited data members.

## Debugging Notes

- 1. Function to overload << operator must return an ostream reference.
- 2. Function to overload >> operator must return an istream reference.
- 3. Derived class must include a set of constructor functions.
- 4. Derived classes do not inherit constructor functions from their base class.

## Problems

## Exam Practice!

## True or False

Indicate whether each of the following is true (T) or false (F).

- 1. The private members of a base class are inaccessible to the derived class. T F
- 2. When an object of a derived class is created, the constructor of the base class is not called. T F
- 3. This pointer is a built-in pointer that always points to the instance of the class making the function call. T F
- 4. Pointers to a base class cannot be assigned the address of a derived class object. T F
- 5. A stand-alone function, a member of another class, or even an entire class could be declared friend of a class and would have access to the all members of the class.

## Multiple Choice

- 6. Which of the following is not true about the notion of friendship in object oriented programming?
- a. Even though the prototypes for friend functions appear in the class definition, friends are not member functions of the class.
- b. A friend declaration can be placed anywhere in a class definition.
- c. The friendship relation is symmetric i.e., if class A is declared a friend of class B, then class B is automatically a friend of class A.
- d. The friendship relation is not transitive, i.e., if class A is a friend of class B, and class B is a friend of class C, then class A cannot be inferred as a friend of class C.

- 7. Which of the following is not true about the static members of a class?
- a. A static member function of a class does not have a this pointer.
- b. A static data member of a class is shared by all instances of the class.
- c. The static members have class scope and can be declared public, private or protected.
- d. The static members of a class can exist when no objects of that class exist and it can be accessed by prefixing the class name and binary scope resolution operator (::) to the name of the data member.
- e. Static member functions of a class can access its non-static data members.

## Programming Problems

- 8. Add a recursive method to the BinaryTree class that returns a count of the number of leaf nodes in the tree.
- 9. Write a program that uses the BinaryTree class to order a set of data read from a data file. Your program should open a data file, read the data and store it in your tree, then print the data using the InOrder print method.
- 10. Download an image from the web and implement a function to “dither” the image by setting every other pixel to black. Do not allow vertical black lines to appear.
- 11. Download an image, and implement the function to fade an image.
