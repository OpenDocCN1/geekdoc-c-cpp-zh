```
class Card {
public:
//Constructors
Card(); //Default
Card(char aSuit, int aRank);//parameterized
//Accessors
int getRank() const;
char getSuit() const;
//Formatted Display Method
//Example: if char is 'S' and rank is 11
//output will be:
//Jack of Spades
void displayCard(ostream& outStream) const;
private:
char suit;
int rank;
};
#endif //end compiler directive ifndef
/*-----------------------------------------------------*/
Card.cpp
/*-----------------------------------------------------*/
/* Card class implementation */
/* filename: Card.cpp */
/*-----------------------------------------------------*/
#include "Card.h" //Required for Card
#include<cctype> //Required for toupper()
#include <string> //Required for string
#include<iostream> //require for ostream
using namespace std;
//Constructors.
Card::Card():rank(2), suit('S')
{
}
Card::Card(char ch, int i): rank(i)
{
suit=toupper(ch);
}
//Accessor Methods
int Card::getRank() const
{
return rank;
}
char Card::getSuit() const
{
return suit;
}
```