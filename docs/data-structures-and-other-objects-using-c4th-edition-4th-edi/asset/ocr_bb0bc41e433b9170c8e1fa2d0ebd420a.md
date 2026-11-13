# Self-Test Exercises for End of Section 14.2

+   12. Write code to declare a vector of organisms. Put 10 new organisms in the vector, with an initial size of 16 ounces and a growth rate of 1 ounce per week. Grab five random organisms, and alter their growth rates to 2 ounces per week. Finally, calculate the total of all the organisms' growth rates, and print the result.

+   13. In the previous exercise, you started with 10 organisms growing at 1 ounce per week. Five random organisms had their growth rates changed to 2 ounces per week, so you might think that the total of all the organisms' rates would be 5*1 + 5*2, which is 15. But when we ran the program, the total was only 14. Why?

+   14. Design and implement a new class derived from the animal class. The new class, called carnivore, has one new member function with the prototype shown here:

```
void carnivore::chase(animal* prey, double chance);
```

When chase(prey, chance) is activated for some carnivore, the carnivore chases the prey. The probability of actually catching the prey is given by the parameter chance (which should lie between 0 and 1—for example 0.75 for a 75% chance). If the prey actually caught, then this will also activate the carnivore's eat member function and (sadly) activate the prey's death member function.

Note: You can use the rand function (from <cstdlib>) to determine whether the animal is caught, as shown here:

```
if (rand() / double(RAND_MAX) < chance)
{
    || Code for catching and eating the prey
}
```

# 14.3 VIRTUAL MEMBER FUNCTIONS AND A GAME CLASS

This section demonstrates virtual member functions, which are a new kind of member function that allows certain aspects of activating a function to be delayed until a program is actually running.

# Introduction to the game Class

To make the explanation of virtual functions concrete, we'll present an example of a class called game, which will make it easier for us to write programs that play various two-player games such as chess, checkers, or Othello. The games we have in mind will pit a human player against the computer, with the computer making moves that are, hopefully, intelligent.