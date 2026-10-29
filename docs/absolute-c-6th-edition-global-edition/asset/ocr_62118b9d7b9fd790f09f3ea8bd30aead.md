should be derived from Demon. You will need to rewrite the getSpecies( ) and getDamage( ) functions so they are appropriate for each class.

For example, the getDamage( ) function in each class should only compute the damage appropriate for that object. The total damage is then calculated by combining the results of getDamage( ) at each level of the inheritance hierarchy. As an example, invoking getDamage( ) for a Balrog object should invoke getDamage( ) for the Demon object, which should invoke getDamage( ) for the Creature object. This will compute the basic damage that all creatures inflict, followed by the random 5% damage that demons inflict, followed by the double damage that balrogs inflict.

Also include mutator and accessor functions for the private variables. Write a main function that contains a driver to test your classes. It should create an object for each type of creature and repeatedly outputs the results of getDamage( ). First, make the getDamage( ) function virtual. Then, make a function in your main program, battleArena( Creature &creature1, Creature &creature2), that takes two Creature objects as input. The function should calculate the damage done by creature1, subtract that amount from creature2’s hit points, and vice versa. If both creatures end up with zero or less hit points, then the battle is a tie. Otherwise, at the end of a round, if one creature has positive hit points but the other does not, then the battle is over. The function should loop until the battle is either a tie or over. Since the getDamage( ) function is virtual, it should invoke the getDamage( ) function defined for the specific creature. Test your program with several battles involving different creatures.

# 5. The following shows code to play a guessing game in which two players attempt to guess a number. Your task is to extend the program with objects that represent either a human player or a computer player.

```
bool checkForWin(int guess, int answer)
{
    if (answer == guess)
    {
        cout << "You're right! You win!" << endl;
        return true;
    }
    else if (answer < guess)
        cout << "Your guess is too high." << endl;
    else
        cout << "Your guess is too low." << endl;
    return false;
}
void play(Player &player1, Player &player2)
{
    int answer = 0, guess = 0;
    answer = rand() % 100;
    bool win = false;
```

![](bbox=[0.07, 0.68, 0.18, 0.82])