Populate() creates a standard deck of 52 cards. The member function loops through all of the possible combinations of Card::suit and Card::rank values. It uses static_cast to cast the int loop variables to the proper enumerated types defined in Card.

Shuffle() shuffles the cards in the deck. It randomly rearranges the pointers in m_Cards with random_shuffle() from the Standard Template Library. This is the reason I include the <algorithm> header file.

Deal() deals one card from the deck to a hand. It adds a copy of the pointer to the back of m_Cards to the object through the object’s Add() member function. Then, it removes the pointer at the back of m_Cards, effectively transferring the card. The powerful thing about Deal() is that it accepts a reference to a Hand object, which means it can work equally well with a Player or a House object. And through the magic of polymorphism, Deal() can call the object’s Add() member function without knowing the exact object type.

AdditionalCards() gives additional cards to a generic player until the generic player either stops hitting or busts. The member function accepts reference to a GenericPlayer object so you can pass a Player or House object to it. Again, through the magic of polymorphism, AdditionalCards() doesn’t have to know whether it’s working with a Player or a House object. It can call the IsBusted() and IsHitting() member functions for the object without knowing the object’s type, and the correct code will be executed.

# The Game Class

The Game class represents a game of Blackjack.

```
class Game
{
public:
    Game(const vector<string>& names);

    ~Game();

    //plays the game of blackjack
    void Play();
```