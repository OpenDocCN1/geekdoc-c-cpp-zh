predicate should be a PlayingCard object (the list contains PlayingCard items).

The updated statements occur after the closing brace of the second while loop, as shown in bold in the following code:

Click here to view code image

```
public PlayingCard DealCardFromPack() {
    Suit suit = (Suit)randomCardSelector.Next (NumSuits);
    while (this.IsSuitEmpty(suit)) {
        suit = (Suit)randomCardSelector.Next (NumSuits);
    }
    Value value = (Value)randomCardSelector.Next (CardsPerSuit);
    while (this.IsCardAlreadyDealt(suit, value)) {
        value = (Value)randomCardSelector.Next (CardsPerSuit);
    }
    List<PlayingCard> cardsInSuit = this.cardPack[suit];
    PlayingCard card = cardsInSuit.Find(c => c.CardValue == value);
    cardsInSuit.Remove(card);
    return card;
```

# 10. Locate the IsCardAlreadyDealt method.

This method determines whether a card has already been dealt by checking whether the corresponding element in the array has been set to null. You need to modify this method to determine whether a card with the specified value is present in the list for the suit in the cardPack Dictionary collection.

To determine whether an item exists in a List<T> collection, you use the Exists method. This method is similar to Find in it takes a predicate as its argument, and it should return true if the item matches each item from the collection, and false otherwise. In this case, the List<T> collection holds PlayingCard objects, and the criteria for the Exists predicate should return true if it is passed a PlayingCard item with a suit and value that matches the parameters passed to the IsCardAlreadyDealt method.

Update the method, as shown in the following example in bold:

Click here to view code image