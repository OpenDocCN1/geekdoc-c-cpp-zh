```
this.cardPack[(int)suit, (int)value] = null;
return card;
}
```

+   17. Locate the IsNotEmpty method. Remember that the purpose of this method is to take a Suit parameter and return a Boolean value indicating whether there are any more cards of this suit left in the pack. Delete the comment and the statement that throws the NotImplementedException from this method, and then add the following code shown in bold:

[Click here to view code image]

```
private bool IsNotEmpty(Suit suit)
{
    bool result = true;
    for (var value = Value.Two; value <= Value.Ace; value++)
    {
        if (!IsCardAlreadyDealt(suit, value))
        {
            result = false;
            break;
        }
    }
    return result;
}
```

This code iterates through the possible card values and uses the IsCardAlreadyDealt method (you'll complete in the next step) to determine whether there's a card left in the cardPack array that has the specified suit and value. If the loop finds a card, the value in the result variable is set to false, and the break statement causes the loop to terminate. If the loop completes without finding a card, the result variable remains set to its initial value of true. The value of the result variable is passed back as the return value of the method.

+   18. Find the IsCardAlreadyDealt method. The purpose of this method is to determine whether the card with the specified suit and value has already been dealt and removed from the pack. You will see later that when the DealCardFromPack method deals a card, it removes the card from the cardPack array and sets the corresponding element to null. Replace the body of this method with the code shown in bold:

[Click here to view code image]