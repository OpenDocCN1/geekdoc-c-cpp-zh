
Next, define a class named CashPayment that is derived from Payment. This class should redefine the paymentDetails function to indicate that the payment is in cash. Include appropriate constructor(s).

Define a class named CreditCardPayment that is derived from Payment. This class should contain member variables for the name on the card, expiration date, and credit card number. Include appropriate constructor(s). Finally, redefine the paymentDetails function to include all credit card information in the printout.

Create a main function that creates at least two CashPayment and two CreditCardPayment objects with different values and calls paymentDetails for each.

## 7.

Define a class named Document that contains a member variable of type string named text that stores any textual content for the document. Create a function named getText that returns the text field, a way to set this value, and an overloaded assignment operator.

Next, define a class for Email that is derived from Document and that includes member variables for the sender, recipient, and title of an e-mail message. Implement appropriate accessor and mutator functions. The body of the e-mail message should be stored in the inherited variable text. Also overload the assignment operator for this class.

Similarly, define a class for File that is derived from Document and that includes a member variable for the pathname. Implement appropriate accessor and mutator functions for the pathname and overload the assignment operator.

Finally, create several sample objects of type Email and File in your main function. Test your objects by passing them to the following subroutine, which will return true if the object contains the specified keyword in the text property.

```
bool ContainsKeyword(const Document& docObject, string keyword)
{
    if (docObject.getText().find(keyword) != string::npos)
        return true;
    return false;
}
```

For example, you might test to see whether an e-mail message contains the text "c++" with the call ContainsKeyword(emailObj, "c++").

## 8.

Create a class for a simple blog. The owner of the blog should be able to (a) post a new message, (b) numerically list and display all messages, and (c) select a specific message and delete it.

Viewers of the blog should only be able to numerically list and display all posted messages.

Create a class Viewer and a class Owner that uses inheritance to help implement the blog functionality. Store the data messages using any format you like (a vector of type string may be easiest). A menu function should be implemented for each class that outputs the legal choices for the type of user. To test your classes, the main function of the program should allow the user to invoke the menus from the Viewer and Owner objects.

## 9.

Suppose that you are creating a fantasy role-playing game. In this game, we have four different types of creatures: humans, cyberdemons, balrogs, and elves. To represent one of these creatures, we might define a Creature class as follows:

```
class Creature
{
    private:
        int type;    // 0 human, 1 cyberdemon, 2 balrog, 3 elf
        int strength;    // How much damage we can inflict
        int hitpoints;   // How much damage we can sustain
        string getSpecies(); // Returns type of species
    public:
        Creature();
        // Initialize to human, 10 strength, 10 hit points
        Creature(int newType, int newStrength, int newHit);
        // Initialize creature to new type, strength, hit points
        // Also add appropriate accessor and mutator functions
        // for type, strength, and hit points
        int getDamage();
        // Returns amount of damage this creature
        // inflicts in one round of combat
};
```

Here is an implementation of the getSpecies() function:

```
string Creature::getSpecies()
{
    switch (type)
    {
        case 0: return "Human";
        case 1: return "Cyberdemon";
        case 2: return "Balrog";
        case 3: return "Elf";
    }
    return "Unknown";
}
```

The getDamage() function outputs and returns the damage this creature can inflict in one round of combat. The rules for calculating the damage are as follows:

- Every creature inflicts damage that is a random number r, where 0 < r <= strength.
- Demons have a 5% chance of inflicting a demonic attack, which is an additional 50 damage points. Balrogs and Cyberdemons are demons.
- Elves have a 10% chance to inflict a magical attack that doubles the normal amount of damage.
- Balrogs are very fast, so they get to attack twice.

An implementation of `getDamage()` is given here:

```
int Creature::getDamage()
{
    int damage;

    // All creatures inflict damage, which is a
    // random number up to their strength
    damage = (rand() % strength) + 1;
    cout << getSpecies() << " attacks for " <<
            damage << " points!" << endl;

    // Demons can inflict damage of 50 with a 5% chance
    if ((type == 2) || (type == 1))
    {
        if ((rand() % 100) < 5)
        {
            damage = damage + 50;
            cout << "Demon attack inflicts 50 "
                    << " additional damage points!" << endl;
        }
    }

    // Elves inflict double magical damage with a 10% chance
    if (type == 3)
    {
        if ((rand() % 10)==0)
        {
            cout << "Magical attack inflicts " << damage <<
                    " additional damage points!" << endl;
            damage = damage * 2;
        }
    }

    // Balrogs are so fast they get to attack twice
    if (type == 2)
    {
        int damage2 = (rand() % strength) + 1;
        cout << "Balrog speed attack inflicts " << damage2 <<
                " additional damage points!" << endl;

        damage = damage + damage2;
    }
    return damage;
}
```

One problem with this implementation is that it is unwieldy to add new creatures. Rewrite the class to use inheritance, which will eliminate the need for the variable type. The Creature class should be the base class. The classes Demon, Elf, and Human should be derived from Creature. The classes Cyberdemon and Balrog should be derived from Demon. You will need to rewrite the getSpecies() and getDamage() functions so they are appropriate for each class.

For example, the getDamage() function in each class should only compute the damage appropriate for that object. The total damage is then calculated by combining the results of getDamage() at each level of the inheritance hierarchy. As an example, invoking getDamage() for a Balrog object should invoke getDamage() for the Demon object, which should invoke getDamage() for the Creature object. This will compute the basic damage that all creatures inflict, followed by the random 5% damage that demons inflict, followed by the double damage that balrogs inflict.

Also include mutator and accessor functions for the private variables. Write a main function that contains a driver to test your classes. It should create an object for each type of creature and repeatedly outputs the results of getDamage().

## 10.

Define a Pet class that stores the pet's name, age, and weight. Add appropriate constructors, accessor functions, and mutator functions. Also define a function named getLifespan that returns a string with the value "unknown lifespan."

Next, define a Dog class that is derived from Pet. The Dog class should have a private member variable named breed that stores the breed of the dog. Add mutator and accessor functions for the breed variable and appropriate constructors. Redefine the getLifespan function to return "Approximately 7 years" if the dog's weight is over 100 pounds and "Approximately 13 years" if the dog's weight is under 100 pounds.

Next, define a Rock class that is derived from Pet. Redefine the getLifespan function to return "Thousands of years."

Finally, write a test program that creates instances of pet rocks and pet dogs that exercise the inherited and redefined functions.

## 11.

Use inheritance and classes to represent a deck of playing cards. Create a Card class that stores the suit (Clubs, Diamonds, Hearts, Spades) and name (e.g., Ace, 2, 10, Jack) along with appropriate accessors, constructors, and mutators.

Next, create a Deck class that stores a vector of Card objects. The default constructor should create objects that represent the standard 52 cards and store them in the vector. The Deck class should have functions to:

- Print every card in the deck.
- Shuffle the cards in the deck. You can implement this by randomly swapping every card in the deck.
- Add a new card to the deck. This function should take a Card object as a parameter and add it to the vector.
- Remove a card from the deck. This removes the first card stored in the vector and returns it.
- Sort the cards in the deck ordered by name.
