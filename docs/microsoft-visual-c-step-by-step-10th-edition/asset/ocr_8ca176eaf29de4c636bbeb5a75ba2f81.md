```
private bool IsCardAlreadyDealt(Suit suit, Value value)
=> (this.cardPack[(int)suit, (int)value] == null);
```

This method returns true if the element in the cardPack array corresponding
to the suit and value is null, and false otherwise.

+   1 The next step is to add the selected playing card to a hand. Open the Hand.cs
file and display it in the Code and Text Editor window. This file contains the
Hand class, which implements a hand of cards (that is, all cards dealt to
player).

This file contains a public const int called HandSize, which is set to
the size of a hand of cards (13). It also contains an array of PlayingCard
objects, which is initialized by using the HandSize constant. Your code will
use the playingCount field to keep track of how many cards the hand
currently has as it is being populated.

Click here to view code image

```
class Hand
    public const int HandSize = 13;
    private PlayingCard[] cards = new PlayingCard[HandSize];
    private int playingCardCount = 0;
}
```

The ToString method generates a string representation of the cards in the
hand. It uses a foreach loop to iterate through the items in the cards array and
calls the ToString method on each PlayingCard object it finds. These strings
are concatenated with a newline character in between (using the
Environment.NewLine constant to specify the newline character) for
formatting purposes.

Click here to view code image

```
public override string ToString()
{
    string result = ""
    foreach (PlayingCard card in this.cards)
    {
        result += $\{card.ToString()}{Environment.NewLine}";
    }
}
```