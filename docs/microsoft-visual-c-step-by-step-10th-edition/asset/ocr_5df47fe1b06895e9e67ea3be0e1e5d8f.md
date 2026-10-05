```
suit = (Suit)randomCardSelector.Next(NumSuits);
}
```

This loop calls the IsSuitEmpty method to determine whether any cards of the specified suit are left in the pack. (You will implement the logic for this method shortly.) If not, it picks another suit at random—or it might actually pick the same suit again—and checks again. The loop repeats the process until it finds a suit with at least one card left.

You have now selected at random a suit with at least one card left. The next task is to pick a card at random in this suit. You can use the number generator to select a card value, but there's no guarantee that the card with the chosen value has not already been dealt. However, you can use the same idiom before: Call the IsCardAlreadyDealt method (which'll examine and complete later). You use this method to determine whether the card has already been dealt, and if so, pick another card at random and try again—repeating the process until card is found.

+   15. Add the following statements shown in bold to the DealCardFromPack method, after the existing code, call the IsCardAlreadyDealt method:

Click here to view code image

```
public PlayingCard DealCardFromPack()
{
  var value = (Value)randomCardSelector.Next(CardsPerSuit);
  while (this.IsCardAlreadyDealt(suit, value))
  {
    value = (Value)randomCardSelector.Next(CardsPerSuit);
  }
}
```

+   16. You have now selected a random playing card that has not been dealt previously. Add the following code to the DealCardFromPack method to return this card and set the corresponding element in the cardPack array to null:

Click here to view code image

```
public PlayingCard DealCardFromPack()
{
  ...
  var card = this.cardPack[(int)suit, (int)value];
```