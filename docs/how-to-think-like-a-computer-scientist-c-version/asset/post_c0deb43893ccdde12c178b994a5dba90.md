
## 13.3 Decks

In the previous chapter, we worked with a vector of objects, but I also mentioned that it is possible to have an object that contains a vector as an instance variable. In this chapter I am going to create a new object, called a Deck, that contains a vector of Cards.

The structure definition looks like this

```cpp
struct Deck {
  avector<Card> cards;

  Deck(int n);
};

Deck::Deck(int size) {
  avector<Card> temp(size);
  cards = temp;
}
```

The name of the instance variable is cards to help distinguish the Deck object from the vector of Cards that it contains.

For now there is only one constructor. It creates a local variable temp, which it initializes by invoking the constructor for the avector class, passing the size as a parameter. Then it copies the vector from temp into the instance variable cards.

We can create a deck of cards like this:

Deck (52):

Here is a state diagram showing what a Deck object looks like:

| | 1 | 2 | 51 |
|---|---|---|---|
| suit: 0 | suit: 0 | suit: 0 |
| rank: 0 | rank: 0 | rank: 0 |

The object named deck has a single instance variable named cards, which is a vector of Card objects. To access the cards in a deck we have to compose the syntax for accessing an instance variable and the syntax for selecting an element from an array. For example, the expression deck.cards[i] is the ith card in the deck, and deck.cards[i].suit is its suit. The following loop

```cpp
for (int i = 0; i<52; i++) {
    deck.cards[i].print();
}
```

demonstrates how to traverse the deck and output each card.

## 13.4 Another constructor

Now that we have a Deck object, it would be useful to initialize the cards in it. From the previous chapter we have a function called buildDeck that we could use (with a few adaptations), but it might be more natural to write a second constructor.

```cpp
Deck::Deck() {
    apvector<Card> temp (52);
    cards = temp;

    int i = 0;
    for (Suit suit = CLUBS; suit <= SPADES; suit = Suit(suit+1)) {
        cards[i].suit = suit;
        cards[i].rank = rank;
        i++;
    }
}
```

Notice how similar this function is to buildDeck, except that we had to change the syntax to make it constructor. Now we can create a standard 52-card deck with the simple declaration Deck deck;

## 13.5 Deck member functions

Now that we have a Deck object, it makes sense to put all the functions that pertain to Deck in the Deck definition. Looking at the functions we have written so far, one obvious candidate is printDeck (Section 12.7). Here's how it works, rewritten as a Deck member function:

```cpp
void Deck::print() const {
    for (int i = 0; i < cards.length(); i++) {
        cards[i].print();
    }
}
```

As usual, we can refer to the instance variables of the current object without using dot notation. For some of the other functions, it is not obvious whether they should be member functions of Card, member functions of Deck, or nonmember functions that take Cards and Deck as parameters. For example, the version of find in the previous chapter takes a Card and a Deck as arguments, but you could reasonably make it a member function of either type. As an exercise, rewrite find as a member function that takes Card as a parameter.

Writing find as a Card member function is a little tricky. Here's my version:

```cpp
int Card::find(const Deck& deck) const {
  for (int i = 0; i < deck.cards.length(); i++) {
    if (equals(deck.cards[i], *this)) return 1;
  }
  return -1;
}
```

The first trick is that we have to use the keyword this to refer to the Card function is invoked on. The second trick is that C++ does not make it easy to write structure definitions that refer to each other. The problem is when the compiler is reading the first structure definition, it doesn't know about the second one yet. One solution is to declare Deck before Card and then define afterwards:

```cpp
// declare that Deck is a structure, without defining it
struct Deck;
```

```cpp
// that we can refer to it in the definition of Card
struct Card {
  int suit, rank;

  Card();
  Card(int s, int r);

  void print() const;
  bool isGreater(const Card& c2) const;
  int find(const Deck& deck) const;
}
```

```cpp
// and then later we provide the definition of Deck
struct Deck {
  apvector<Card> cards;
  Deck ();
  Deck (int n);
  void print () const;
  int find (const Card& card) const;
};
```

## 13.6 Shuffling

For most games you need to be able to shuffle the deck; that is, put the cards in a random order. In Section 10.5 we saw how to generate random numbers, but it is not obvious how to use them to shuffle. One possibility is to shuffle the deck by picking a random card and swapping it with the first card, then picking a random card from the remaining and swapping it with the second card, and so on.

Here is an outline of how this algorithm works:

```cpp
for (int i = 0; i < 51; i++) {
    int j = randomInt(i, 51);
    swap(cards[i], cards[j]);
}
```

The nice thing about this algorithm is that it only requires one pass through the deck and is easy to implement.

## 13.7 Sorting

Now that we have messed up the deck, we need a way to put it back in order. Ironically, there is an algorithm for sorting that is very similar to the shuffling. The only difference is that instead of choosing the card at random, we find the lowest card in the deck.

```cpp
for (int i = 0; i < cards.length() - 1; i++) {
    int min_index = i;
    for (int j = i + 1; j < cards.length(); j++) {
        if (cards[j] < cards[min_index]) {
            min_index = j;
        }
    }
    swap(cards[i], cards[min_index]);
}
```

Again, the pseudocode helps with the design of the helper functions. In this case we can use swapCards again, so we need only one new, called findLowest, that takes a vector of cards and an index

## 13.8 Subdecks

How we represent a hand or other subset of a full deck? One easy choice is to make a Deck object that has fewer than 52 cards. We want a function, subdeck, that takes a vector of cards and a indices, and returns a vector of cards that contains the specified subdeck of the deck:

```cpp
Deck::subdeck(int low, int high) const {
  Deck sub(high-low+1);
  for (int i = 0; i<sub.cards.length(); i++) {
    sub.cards[i] = cards[low+i];
  }
  return sub;
}
```

To create the local variable subdeck we are using the Deck constructor that takes the size of the deck as an argument and does not initialize the cards. The cards are initialized when they are copied from the original deck. The length of the deck is high-low+1 because both the low card and high card are included. This sort of computation is confusing, and can lead to “off-by-one” errors. Drawing a picture is usually the best way to avoid them.
