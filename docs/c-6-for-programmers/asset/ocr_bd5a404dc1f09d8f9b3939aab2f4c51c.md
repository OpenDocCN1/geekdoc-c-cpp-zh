lines 14–22 deals all 52 Cards in the deck and displays them in four columns of 13 Cards each. Line 16 deals and displays a Card object by invoking myDeckOfCards.DealCard method. When a Card object is placed in a string-interpolation expression, the Card’s ToString method is invoked implicitly. Because the field width is negative, the result is displayed left-aligned in a field of width 19.

```
```csharp
1  // Fig. 8.12: DeckOfCardsTest.cs
2  // Card-shuffling-and-dealing app.
3  using System;
4
5  class DeckOfCardsTest
6  {
7     // execute app
8     static void Main()
9     {
10       var myDeckOfCards = new DeckOfCards();
11       myDeckOfCards.Shuffle(); // place cards in random order
12
13       // display all 52 Cards in the order in which they are dealt
14       for (var i = 0; i < 52; ++i)
15       {
16          Console.Write($"{myDeckOfCards.DealCard(),-19}");
17
18          if ((i + 1) % 4 == 0)
19          {
20             Console.WriteLine();
21          }
22       }
23    }
24  }
```
```

|  |  |  |  |
|---|---|---|---|
| Eight of Clubs | Ten of Clubs | Ten of Spades | Four of Spades |
| Ace of Spades | Jack of Spades | Three of Spades | Seven of Spades |
| Three of Diamonds | Five of Hearts | Eight of Spades | Five of Hearts |
| Ace of Hearts | Ten of Hearts | Deuce of Hearts | Deuce of Clubs |
| Jack of Hearts | Nine of Spades | Four of Hearts | Seven of Clubs |
| Queen of Spades | Seven of Diamonds | Five of Diamonds | Ace of Clubs |
| Four of Clubs | Ten of Diamonds | Jack of Clubs | Six of Diamonds |
| Eight of Diamonds | King of Hearts | Three of Clubs | King of Spades |
| King of Diamonds | Six of Spades | Deuce of Spades | Five of Spades |
| Queen of Clubs | King of Clubs | Queen of Hearts | Seven of Hearts |
| Ace of Diamonds | Deuce of Diamonds | Four of Diamonds | Nine of Clubs |
| Queen of Diamonds | Jack of Diamonds | Six of Hearts | Nine of Diamonds |
| Nine of Hearts | Three of Hearts | Six of Clubs | Eight of Hearts |

Fig. 8.12 | Card-shuffling-and-dealing app.

# ## 8.7 Passing Arrays and Array Elements to Methods

To pass an array argument to a method, specify the name of the array *without any brackets*. For example, if hourlyTemperatures is declared as

```
```csharp
var hourlyTemperatures = new double[24];
```
```