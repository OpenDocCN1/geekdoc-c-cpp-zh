```
Cards tempHand = (Cards)PlayHand.Clone();
// find three and four of a kind sets
bool fourOfAKind = false;
bool threeOfAKind = false;
int fourRank = -1;
int threeRank = -1;
int cardsOfRank;
for (int matchRank = 0; matchRank < 13; matchRank++)
{
    cardsOfRank = 0;
    foreach (Card c in tempHand)
    {
        if (c.rank == (Rank)matchRank)
        {
            cardsOfRank++;
        }
    }
    if (cardsOfRank == 4)
    {
        // mark set of four
        fourRank = matchRank;
        fourOfAKind = true;
    }
    if (cardsOfRank == 3)
    {
        // two threes means no win possible
        // (threeOfAKind will be true only if this code
        // has already executed)
        if (threeOfAKind == true)
        {
            return false;
        }
        // mark set of three
        threeRank = matchRank;
        threeOfAKind = true;
    }
}
// check simple win condition
if (threeOfAKind && fourOfAKind)
{
    return true;
}
// simplify hand if three or four of a kind is found,
// by removing used cards
if (fourOfAKind || threeOfAKind)
{
    for (int cardIndex = tempHand.Count - 1; cardIndex >= 0; cardIndex--)
    {
        if ((tempHand[cardIndex].rank == (Rank)fourRank)
            || (tempHand[cardIndex].rank == (Rank)threeRank))
        {
            tempHand.RemoveAt(cardIndex);
        }
    }
}
// at this point the method may have returned, because:
// - a set of four and a set of three has been found, winning.
```