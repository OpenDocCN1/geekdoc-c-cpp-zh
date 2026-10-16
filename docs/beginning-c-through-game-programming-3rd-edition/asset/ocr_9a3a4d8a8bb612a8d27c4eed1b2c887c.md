# The Critter Class

The Critter class is the blueprint for the object that represents the player’s critter. The class isn’t complicated, and most of it should look familiar, but it’s long enough that it makes sense to attack it in pieces.

# The Class Definition

After some initial comments and statements, I begin the Critter class.

```
//Critter Caretaker
//Simulates caring for a virtual pet

#include <iostream>

using namespace std;

class Critter
{
public:
    Critter(int hunger = 0, int boredom = 0);
    void Talk();
    void Eat(int food = 4);
    void Play(int fun = 4);

private:
    int m_Hunger;
    int m_Boredom;

    int GetMood() const;
    void PassTime(int time = 1);
};
```

m_Hunger is a private data member that represents the critter’s hunger level while m_Boredom is a private data member that represents its boredom level. I’ll go through each member function in its own section.

# The Class Constructor

The constructor takes two arguments, hunger and boredom. The arguments each have a default value of zero, which I specified in the constructor prototype back