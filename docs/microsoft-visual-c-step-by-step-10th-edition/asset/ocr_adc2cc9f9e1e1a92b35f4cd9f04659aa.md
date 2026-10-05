```
hands [handNum].AddCardToHand(cardDealt);
}
}
catch (Exception ex)
{
...
}
```

The inner `for` loop populates each hand by using the `DealCardFromPack` method to retrieve a card at random from the pack and the `AddCardToHand` method to add this card to a hand.

+   26. Add the following code shown in bold after the outer `for` loop:

Click here to view code image

The cards in the pack should be dealt at random to each hand, and the cards in each hand should be displayed on the form, similarly as shown in the