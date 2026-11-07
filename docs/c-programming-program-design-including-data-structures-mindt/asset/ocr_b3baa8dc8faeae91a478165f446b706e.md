```
```cpp
circle2.setRadius(radius);                         //Line 16

cout << "Line 17: After setting the radius."
     << endl;                                      //Line 17

cout << "Line 18: circle2 - "
     << "radius: " << circle2.getRadius()
     << ", area: " << circle2.area()
     << ", circumference: "
     << circle2.circumference() << endl;            //Line 18

        return 0;                                  //Line 19
} //end main                                      //Line 20
```
```

**Sample Run:** In this sample run, the user input is shaded.

Line 11: circle1 - radius: 8.00, area: 201.06, circumference: 50.27

Line 12: circle2 - radius: 0.00, area: 0.00, circumference: 0.00

Line 13: Enter the radius: 6.25

Line 17: After setting the radius.

Line 18: circle2 - radius: 6.25, area: 122.72, circumference: 39.27

The preceding program works as follows. The statements in Lines 7 and 8 create the objects circle1 and circle2. The radius of circle1 is set to 8; and the radius of circle2 is set to 0 by using the default value by the constructor. The statements in Lines 11 and 12 output the data of circle1 and circle2. The statements in Lines 13 and 14 prompt the user to enter the radius of a circle and store the radius in the variable radius. The statement in Line 16 uses the member function setRadius and the value of radius to set the radius of circle2. The statement in Line 18 outputs the (new) data of circle2.

# EXAMPLE 10-9

In Example 6-4, in Chapter 6, the function rollDice rolls a pair of dice until the sum of the numbers rolled is a given number. It then returns the number of times the dice are rolled to get the desired sum. In fact, we can design a class that implements the basic properties of a die. Consider the definition of the following class die.

```
```cpp
class die
{
public:
    die();
        //Default constructor
        //Sets the default number rolled by a die to 1

    void roll();
        //Function to roll a die
        //This function uses a random number generator to randomly
```
```