
# Table 10.6 House Class

| Member | Description |
|---|---|
| virtual bool IsHitting() const | Indicates whether the house is taking another hit. |
| void FlipFirstCard() | Flips over the first card. |

# Table 10.7 Deck Class

| Member | Description |
|---|---|
| void Populate() | Creates a standard deck of 52 cards. |
| void Shuffle() | Shuffles cards. |
| void Deal(Hand& aHand) | Deals one card to a hand. |
| void AdditionalCards(GenericPlayer& aGenericPlayer) | Gives additional cards to a generic player for as long as the generic player can and wants to hit. |

# Table 10.8 Game Class

| Member | Description |
|---|---|
| Deck m_Deck | A deck of cards. |
| House m_House | The casino’s hand, the house. |
| vector<Player> m_Players | Collection of human players. A vector of Player objects. |
| void Play() | Plays a round of Blackjack. |

## Planning the Game Logic

The last part of my planning is to map out the basic flow of one round of the game. I wrote some pseudocode for the Game class’ Play() member function. Here’s what I came up with:

- Deal players and the house two initial cards
- Hide the house's first card
- Display players' and house's hands
- Deal additional cards to players

```
Reveal house's first card
Deal additional cards to house
If house is busted
    Everyone who is not busted wins
Otherwise
    For each player
        If player isn't busted
            If player's total is greater than the house's total
                Player wins
            Otherwise if player's total is less than house's total
                Player loses
            Otherwise
                Player pushes
Remove everyone's cards
```

At this point you know a lot about the Blackjack program and you haven’t even seen a single line of code yet! But that’s a good thing. Planning can be as important as coding (if not more so). Because I’ve spent so much time describing the classes, I won’t describe every part of the code. I’ll just point out significant or new ideas. You can download the code for this program from the Course Technology website (www.courseptr.com/downloads). The program is in the Chapter 10 folder; the filename is blackjack.cpp.

## Hint

The blackjack.cpp file contains seven classes. In C++ programming, it’s common to break up files like this into multiple files, based on individual classes. However, the topic of writing a single program using multiple files is beyond the scope of this book.

## The Card Class

After some initial statements, I define the Card class for an individual playing card.

```
//Blackjack
//Plays a simple version of the casino game of blackjack; for 1 - 7 players

#include <iostream>
#include <string>
#include <vector>
#include <algorithm>
```

```
#include <ctime>

using namespace std;
class Card
{
public:
    enum rank {ACE = 1, TWO, THREE, FOUR, FIVE, SIX, SEVEN, EIGHT, NINE, TEN,
                JACK, QUEEN, KING};
    enum suit {CLUBS, DIAMONDS, HEARTS, SPADES};

    //overloading << operator so can send Card object to standard output
    friend ostream& operator<<(ostream& os, const Card& aCard);

    Card(rank r = ACE, suit s = SPADES, bool ifu = true);

    //returns the value of a card, 1 - 11
    int GetValue() const;

    //flips a card; if face up, becomes face down and vice versa
    void Flip();

private:
    rank m_Rank;
    suit m_Suit;
    bool m_IsFaceUp;
};

Card::Card(rank r, suit s, bool ifu): m_Rank(r), m_Suit(s), m_IsFaceUp(ifu)
{

int Card::GetValue() const
{
    //if a cards is face down, its value is 0
    int value = 0;
    if (m_IsFaceUp)
    {
        //value is number showing on card
        value = m_Rank;
        //value is 10 for face cards
        if (value > 10)
```

```
{
    value = 10;
}
}
return value;
}

void Card::Flip()
{
    m_IsFaceUp = !(m_IsFaceUp);
}
```

I define two enumerations, rank and suit, to use as the types for the rank and suit data members of the class, m_Rank and m_Suit. This has two benefits. First, it makes the code more readable. A suit data member will have a value like CLUBS or HEARTS instead of 0 or 2. Second, it limits the values that these two data members can have. m_Suit can only store a value from suit, and m_Rank can only store a value from rank.

Next, I make the overloaded operator<<() function a friend of the class so I can display a card object on the screen.

GetValue() returns a value for a Card object, which can be between 0 and 11. Aces are valued at 11. (I deal with potentially counting them as 1 in the Hand class, based on the other cards in the hand.) A face-down card has a value of 0.

## The Hand Class

I define the Hand class for a collection of cards.

```
class Hand
{
public:
    Hand();

    virtual ~Hand();

    //adds a card to the hand
    void Add(Card* pCard);

    //clears hand of all cards
    void Clear();
```

```
//gets hand total value, intelligently treats aces as 1 or 11
int GetTotal() const;

protected:
    vector<Card*> m_Cards;
};

Hand::Hand()
{
    m_Cards.reserve(7);
}

Hand::~Hand()
{
    Clear();
}

void Hand::Add(Card* pCard)
{
    m_Cards.push_back(pCard);
}

void Hand::Clear()
{
    //iterate through vector, freeing all memory on the heap
    vector<Card*>::iterator iter = m_Cards.begin();
    for (iter = m_Cards.begin(); iter != m_Cards.end(); ++iter)
    {
        delete *iter;
        *iter = 0;
    }
    //clear vector of pointers
    m_Cards.clear();
}

int Hand::GetTotal() const
{
    //if no cards in hand, return 0
    if (m_Cards.empty())
    {
        return 0;
```
```

```
//if a first card has value of 0, then card is face down; return 0
if (m_Cards[0]->GetValue() == 0)
{
    return 0;
}

//add up card values, treat each ace as 1
int total = 0;
vector<Card*>::const_iterator iter;
for (iter = m_Cards.begin(); iter != m_Cards.end(); ++iter)
{
    total += (*iter)->GetValue();
}

//determine if hand contains an ace
bool containsAce = false;
for (iter = m_Cards.begin(); iter != m_Cards.end(); ++iter)
{
    if ((*iter)->GetValue() == Card::ACE)
    {
        containsAce = true;
    }
}

//if hand contains ace and total is low enough, treat ace as 11
if (containsAce && total <= 11)
{
    //add only 10 since we've already added 1 for the ace
    total += 10;
}

return total;
}
```

## Trap

The destructor of the class is virtual, but notice that I don’t use the keyword virtual outside of the class when I actually define the destructor. You only use the keyword inside the class definition. Don’t worry; the destructor is still virtual.

Although I’ve already covered this, I want to point it out again. All of the Card objects will exist on the heap. Any collection of cards, such as a Hand object, will have a vector of pointers to a group of those objects on the heap.

The Clear() member function has an important responsibly. It not only removes all of the pointers from the vector m_Cards, but it destroys the associated Card objects and frees the memory on the heap that they occupied. This is just like a real-world Blackjack game in which cards are discarded when a round is over. The virtual class destructor calls Clear().

The GetTotal() member function returns the point total of the hand. If a hand contains an ace, it counts it as a 1 or an 11, whichever is best for the player. The program accomplishes this by checking to see whether the hand has at least one ace. If it does, it checks to see whether treating the ace as 11 will put the hand’s point total over 21. If it won’t, then the ace is treated as an 11. Otherwise, it’s treated as a 1.

## The GenericPlayer Class

I define the GenericPlayer class for a generic Blackjack player. It doesn’t represent a full player. Instead, it represents the common element of a human player and the computer player.

```
class GenericPlayer : public Hand
{
    friend ostream& operator<<(ostream& os,
                                const GenericPlayer& aGenericPlayer);

public:
    GenericPlayer(const string& name = "");

    virtual ~GenericPlayer();

    //indicates whether or not generic player wants to keep hitting
    virtual bool IsHitting() const = 0;

    //returns whether generic player has busted - has a total greater than 21
    bool IsBusted() const;

    //announces that the generic player busts
    void Bust() const;
```
