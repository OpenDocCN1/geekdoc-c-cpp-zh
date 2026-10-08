# 358 Chapter 8 Arrays; Introduction to Exception Handling

```
4 class DeckOfCards
6 {
7 // create one Random object to share among DeckOfCards objects
8 private static Random randomNumbers = new Random();
9
10 private int NumberOfCards = 52; // number of cards in a deck
11 Card[] deck = new Card[NumberOfCards];\12 private int currentCard = 0; // index of next card to be dealt (0-51)
13
14 // constructor fills deck of Cards
15 public DeckOfCards() {
16 string[] faces = {"Ace","Deuce","Three","Four","Five","Six",
17 "Seven","Eight","Nine","Ten","Jack","Queen","King"};
18 string[] suits = {"Hearts","Diamonds","Clubs","Spades"};
19
20 // populate deck with Card objects
21 for (var count = 0; count < deck.Length; count++)
22 {
23 deck[count] = new Card(faces[count % 13], suits[count / 13]);
24 }
25
26 // shuffle deck of Cards with one-pass algorithm
27 public void Shuffle() {
28
29 // after shuffling, dealing should start at deck[0] again
30 currentCard = 0; // reinitialize currentCard
31
32 // for each card, pick another random Card and swap them
33 for (var first = 0; first < deck.Length; ++first)
34 {
35 // select a random number between 0 and 51
36 var second = randomNumbers.Next(NumberOfCards);
37
38 // swap current Card with randomly selected Card
39 Card temp = deck[first];
40 deck[first] = deck[second];
41 deck[second] = temp;
42 }
43 }
4
45 // deal one Card
46 public Card DealCard() {
47
48 // determine whether remain to be dealt
49 if (currentCard < deck.Length)
50 return deck[currentCard++]; // return current Card in array
51 }
52 else
53 {
```

Fig. 8.11 | DeckOfCards class represents a deck of playing cards. (Part 2 of 3.)