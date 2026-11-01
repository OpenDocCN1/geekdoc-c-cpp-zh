```
public static bool operator <(Card card1, Card card2)
    => !(card1 > card2);
public static bool operator >=(Card card1, Card card2)
{
    if (card1.suit == card2.suit)
    {
        if (isAceHigh)
        {
            if (card1.rank == Rank.Ace)
            {
                return true;
            }
            else
            {
                if (card2.rank == Rank.Ace)
                    return false;
                else
                    return (card1.rank >= card2.rank);
            }
        }
        else
        {
            return (card1.rank >= card2.rank);
        }
    }
    else
    {
        if (useTrumps && (card2.suit == Card.trump))
            return false;
        else
            return true;
    }
}
public static bool operator <=(Card card1, Card card2)
    => !(card1 > card2);
```

There's not much to note here, except perhaps the slightly lengthy code for the > and >= overloaded operators. If you step through the code for >, you can see how it works and why these steps are necessary.

You are comparing two cards, card1 and card2, where card1 is assumed to be the first one laid down on the table. As discussed earlier, this becomes important when you are using trump cards, because a trump will beat a non-trump even if the non-trump has a higher rank. Of course, if the suits of the two cards are identical, then whether the suit is the trump suit or not is irrelevant, so this is the first comparison you make:

```
public static bool operator >(Card card1, Card card2)
{
    if (card1.suit == card2.suit)
    {
```