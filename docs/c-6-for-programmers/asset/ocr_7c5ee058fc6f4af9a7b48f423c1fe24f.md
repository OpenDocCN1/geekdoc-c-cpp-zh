```
// constructor fills deck of Cards
public DeckOfCards()
{
string[] faces = {"Ace", "Deuce", "Three", "Four", "Five", "Six", "Seven", "Eight", "Nine", "Ten", "Jack", "Queen", "King"};
string[] suits = {"Hearts", "Diamonds", "Clubs", "Spades"};

// populate deck with Card objects
for (var count = 0; count < deck.Length; ++count)
{
deck[count] = new Card(faces[count % 13], suits[count / 13]);
}

// shuffle deck of Cards with one-pass algorithm
public void Shuffle()
{
// after shuffling, dealing should start at deck[0] again
currentCard = 0; // reinitialize currentCard

// for each Card, pick another random Card and swap them
for (var first = 0; first < deck.Length; ++first)
{
// select a random number between 0 and 51
var second = randomNumbers.Next(NumberOfCards);

// swap current Card with randomly selected Card
Card temp = deck[first];
deck[first] = deck[second];
deck[second] = temp;
}
}

// deal one Card
public Card DealCard()
{
// determine whether Cards remain to be dealt
if (currentCard < deck.Length)
{
return deck[currentCard++]; // return current Card in array
}
else
{
return null; // indicate that all Cards were dealt
}
}
}
```

Fig. 8.11 | DeckOfCards class represents a deck of playing cards. (Part 2 of 2.)

# Class DeckOfCards: Constructor

The constructor (lines 22–25) fills the deck array with Cards. The for statement initializes count to 0 and loops while count is less than deck.Length, causing count to take on each integer value from 0 to 51 (the deck array’s indices). Each Card is initialized with two