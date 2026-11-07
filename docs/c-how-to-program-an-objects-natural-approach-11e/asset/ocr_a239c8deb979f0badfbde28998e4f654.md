+   b) An integer currentCard representing the next card to deal.
+   c) A default constructor that initializes the Cards in the deck.
+   d) A shuffle function that shuffles the Cards in the deck. The shuffle algorithm should iterate through the array of Cards. For each Card, randomly select another Card in the deck and swap the two Cards.
+   e) A dealCard function that returns the next Card object from the deck.
+   f) A moreCards function that returns a bool value indicating whether there are more Cards to deal.

The driver program should create a DeckOfCards object, shuffle the cards, then deal the 52 cards—the output should be similar to the following:

| | | | |
|---|---|---|---|
| Six of Spades | Eight of Spades | Six of Clubs | Nine of Hearts |
| Queen of Hearts | Seven of Clubs | Nine of Spades | King of Hearts |
| Three of Diamonds | Deuce of Clubs | Ace of Hearts | Ten of Spades |
| Four of Spades | Ace of Clubs | Seven of Diamonds | Four of Hearts |
| Three of Clubs | Deuce of Hearts | Five of Spades | Jack of Diamonds |
| King of Clubs | Ten of Hearts | Three of Hearts | Six of Diamonds |
| Queen of Clubs | Eight of Diamonds | Deuce of Diamonds | Ten of Diamonds |
| Three of Spades | King of Diamonds | Nine of Clubs | Six of Hearts |
| Ace of Spades | Four of Diamonds | Seven of Hearts | Eight of Clubs |
| Deuce of Spades | Eight of Hearts | Five of Hearts | Queen of Spades |
| Jack of Hearts | Seven of Spades | Four of Clubs | Nine of Diamonds |
| Ace of Diamonds | Queen of Diamonds | Five of Clubs | King of Spades |
| Five of Diamonds | Ten of Clubs | Jack of Spades | Jack of Clubs |

**9.25** *(Card Shuffling and Dealing)* Modify the program you developed in Exercise 9.24 so that it deals a five-card poker hand. Then write functions to accomplish each of the following:

+   a) Determine whether the hand contains a pair.
+   b) Determine whether the hand contains two pairs.
+   c) Determine whether the hand contains three of a kind (e.g., three jacks).
+   d) Determine whether the hand contains four of a kind (e.g., four aces).
+   e) Determine whether the hand contains a flush (i.e., all five cards of the same suit).
+   f) Determine whether the hand contains a straight (i.e., five cards of consecutive face values).

**9.26** *(Project: Card Shuffling and Dealing)* Use the functions from Exercise 9.25 to write a program that deals two five-card poker hands, evaluates each hand and determines which is the better hand.

**9.27** *(Project: Card Shuffling and Dealing)* Modify the program you developed in Exercise 9.26 so that it can simulate the dealer. The dealer’s five-card hand is dealt “face down” so the player cannot see it. The program should then evaluate the dealer’s hand, and, based on the quality of the hand, the dealer should draw one, two or three more cards to replace the corresponding number of unneeded cards in the original hand. The program should then reevaluate the dealer’s hand.

**9.28** *(Project: Card Shuffling and Dealing)* Modify the program you developed in Exercise 9.27 so that it handles the dealer’s hand, but the player is allowed to decide which cards of the player’s hand to replace. The program should then evaluate both hands and