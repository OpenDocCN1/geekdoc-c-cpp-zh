
4. This Programming Project requires that you first complete Programming Project 14.9 from Chapter 14.

```cpp
class Creature {
private:
    int type; // 0 human, 1 cyberdemon, 2 balrog, 3 elf
    int strength; // How much damage we can inflict
    int hitpoints; // How much damage we can sustain
    string getSpecies(); // Returns type of species
public:
    Creature();
    // Initialize to human, 10 strength, 10 hit points
    Creature(int newType, int newStrength, int newHit);
    // Initialize to new type, strength, hit points
    // Also add appropriate accessor and mutator functions
    // for type, strength, and hit points
    int getDamage();
    // Returns amount of damage this creature
    // inflicts in one round of combat
}
```

Here is an implementation of the getSpecies() function:

```cpp
string Creature::getSpecies() {
    switch (type) {
    case 0: return "Human";
    case 1: return "Cyberdemon";
    case 2: return "Balrog";
    case 3: return "Elf";
    }
    return "Unknown";
}
```

The getDamage() function outputs and returns the damage this creature can inflict in one round of combat. Rules for calculating the damage are as follows:

- Every creature inflicts damage that is a random r, where 0<r<=strength.
- Demons have a 5% chance of inflicting a demonic attack, which is an additional 50 damage points. Balrogs and Cyberdemons are demons.
- Elves have a 10% chance to inflict a magical attack that doubles the normal amount of damage.
- Balrogs are very fast, so they get to attack twice.

An implementation of getDamage() is given here:

```cpp
int Creature::getDamage() {
  int damage;
  // All creatures inflict damage, which is a
  // random number up to their strength
  damage = (rand() % strength) + 1;
  cout << getSpecies() << " attacks for "
         << damage << "points!" << endl;

  // Demons can inflict damage of 50 with a 5% chance
  if ((type == 2) || (type == 1)) {
    if (rand() % 100 < 5) {
      damage = damage + 50;
      cout << "Demonic attack inflicts 50 "
           << "additional damage points!" << endl;
    }
  }
```

```cpp
// Elves inflict double damage with a 10% chance
if (type == 3) {
  if (rand() % 100 == 0) {
    cout << "Magical attack inflicts " <<
         <<"additional damage points!" << endl;
    damage = damage * 2;
  }
}
```

```cpp
// Balrogs are so fast they get to attack twice
if (type == 2) {
  int damage2 = (rand() % strength) + 1;
  cout << "Balrog attack inflicts " << damage2<<
       <<"additional damage points!" << endl;
  damage = damage + damage2;
}
return damage;
```

One problem with this implementation is that it is unwieldy to add new creatures. Rewrite it to use inheritance, which will eliminate the need for the type variable. The Creature class should be the base. The classes Demon, Elf, and Human should be derived from Creature. The classes Cyberdemon and Balrog should be derived from Demon. You will need to rewrite the getSpecies() and getDamage() functions so they are appropriate for each class. For example, the getDamage() function in each class should only compute the damage appropriate for that object. The total damage is then calculated by combining the results of getDamage() at each level of inheritance. For example, invoking getDamage() for a Balrog object should invoke getDamage() for the Demon object, which should invoke getDamage() for the Creature object. This will compute the basic damage that all creatures inflict, followed by the random 5% damage that demons inflict, followed by double damage elves inflict. Also include mutator and accessor functions for the private variables. Write a main function to test your classes. It should create an object for each type of creature and repeatedly outputs the results of getDamage(). First, make getDamage() function virtual. Then, make a function in your program, battleArena(Creature& creature, Creature& creature2), that takes Creature objects as input. The function should calculate the damage, subtract that from creature2's points, and vice versa. If both end up with zero or less points, the battle is a tie. Otherwise, at the end of a round, if one creature has positive points but the other does not, the battle is over. The function should loop until the battle is either a tie or over. Since the getDamage() function is virtual, it should invoke getDamage() defined for the specific creature. Test your program with several battles.

- 5. The following shows code to play a guessing game in which two players attempt to guess a number. Your task is to extend the program with objects that represent either a human player or a computer player.

```cpp
bool checkForWin(int guess, int answer) {
    if (answer == guess) {
        cout << "You're right! win!" << endl;
        return true;
    }
    else if (answer < guess) {
        cout << "Your guess is too high." << endl;
    } else {
        cout << "Your guess is too low." << endl;
    }
    return false;
}
void player(Player& player1, Player& player2) {
    int answer = 0, guess = 0;
    answer = rand() % 100;
    bool win = false;
```

![](img/f4bfc3d28ec32a6e3350e28466e0d1_718_0.png)

```cpp
while (!win)
{
    cout << "Player 1's turn to guess." << endl;
    guess = player1.getGuess();
    win = checkForWin(guess, answer);
    if (win) return;
}
```

```cpp
cout << "Player 2's turn to guess." << endl;
guess = player2.getGuess();
win = checkForWin(guess, answer);
```

The play function takes input as two Player objects. Define the Player class with a virtual function named getGuess(). The implementation of Player::getGuess() can simply return 0. Next, define a class named HumanPlayer derived from Player. The implementation of HumanPlayer::getGuess() should prompt the user to enter a number and return the value entered from the keyboard. Next, define a class ComputerPlayer derived from Player. The implementation of ComputerPlayer::getGuess() should randomly select a number from 0 to 100. Finally, construct a main function that invokes play(Player &player1, &player2) with two instances of a HumanPlayer (human versus), an instance of HumanPlayer and ComputerPlayer (human computer), and two instances of ComputerPlayer (computer versus).

- 6. The computer player in Programming Project 1.5 does not play the number guessing game well, since it makes only random guesses. Modify the program so that the computer plays a more informed game. The specific strategy is up to you, but you must add function() to the Player and ComputerPlayer classes so that play(Player &player1, &player2) can send the result of a guess back to the computer. In other words, the computer must be told if its guess was too high or too low, and it must be told if its opponent's last guess was too high or too low. The computer can then use this information to revise its next guess.

- 7. The following lists a Dice class that simulates rolling a die with a different number of sides. The default is a die with six sides. The roll function simulates two dice objects and returns the sum of their values. The roll function requires including cstdlib.h.

```cpp
class Dice
{
public:
    Dice();
    Dice(int numSides);
    virtual int rollDie() const;
protected:
    int numSides;
}
```

![](img/f4bfc3d28ec32a6e3350e28466e0d1_719_0.png)

```cpp
Dice::Dice()
{
    numSides = 6;
    srand(time(NULL)); // Seeds random number generator
}
Dice::Dice(int numSides)
{
    this->numSides = numSides;
    srand(time(NULL)); // Seeds random number generator
}
int Dice::rollDie() const
{
    return rand() % numSides + 1;
}
// Take two dice objects, roll them, and return the sum
int rollTwoDice(const Dice& die1, const Dice& die2)
{
    return die1.rollDie() + die2.rollDice();
}
```

Write a main function that creates two Dice objects with a number of sides of your choosing. Invoke the rollTwoDice function in a loop that iterates ten times and verify that the functions are working as expected.

Next create your class, LoadedDice, that is derived from Dice. Add a default constructor and a constructor that takes the number of sides as input. Override the rollDice function in LoadedDice so that with a 50% chance the function returns the largest number possible (i.e., numSides), otherwise it returns what Dice's rollDice function returns.

Test your class by replacing the Dice objects in main with LoadedDice objects. You should not need to change anything else. There should be many more dice rolls with the highest possible value. Polymorphism results in LoadedDice's rollDice function to be invoked instead of Dice's rollDice function inside rollTwoDice.
