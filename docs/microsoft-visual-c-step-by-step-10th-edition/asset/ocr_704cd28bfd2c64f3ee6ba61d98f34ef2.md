This class has two readonly fields that represent the value and suit of the card. The constructor initializes these fields.

> A readonly field is useful for modeling data that should not change after it has been initialized. You can assign a value to a readonly field by using an initializer when you declare it or in a constructor, but thereafter you cannot modify it.

The class contains a pair of methods, CardValue and CardSuit, that return this information and overrides the ToString method to return a string representation of the card.

> The CardValue and CardSuit methods are actually better implemented as properties, which you'll learn about in Chapter 15.

+   10. Open the Pack.cs file in the Code and Text Editor window.
This file contains the Pack class, which models a pack of playing cards. At the top of the Pack class are public const int fields called NumSuits and CardsPerSuit. These two fields specify the number of suits in a pack of cards and the number of cards in each.
The private cardPack variable is a two-dimensional array of PlayingCard objects. You'll use the first dimension to specify the suit and the second dimension to specify the value of the card in the suit.
The randomCardSelector variable is a random number generated based on the Random class. You'll use the randomCardSelector variable to help shuffle the cards before they're dealt to each hand.

Click here to view code image