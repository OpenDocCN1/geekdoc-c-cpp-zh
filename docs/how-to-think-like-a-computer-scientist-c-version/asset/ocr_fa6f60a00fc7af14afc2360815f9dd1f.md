CHAPTER 13. OBJECTS OF VECTORS

for shuffling.
Again, we are going to traverse the deck and at each location choose another
card and swap. The only difference is that this time instead of choosing the other
card at random, we are going to find the lowest card remaining in the deck.
By “remaining in the deck,” I mean cards that are at or to the right of the
index i.

```
for (int i=0; icards.length(); i++) {
// find the lowest card at or to the right of i
// swap the ith card at or the lowest card
```

Again, the pseudocode helps with the design of the helper functions. In
this case we can use swapCards again, so we need only one new, called
findLowestCard, that takes a vector of cards and an index where it should
starting.
This process, using pseudocode to figure out what helper functions are
needed, sometimes called top-down design, in contrast to the bottom-up
design discussed in Section 10.8.
Once again, I am going to leave the implementation up to the reader.

# 13.8 Subdecks

How we represent a hand or other subset of a full deck? One easy
choice is to make a Deck object that has fewer than 52 cards.
We want a function, subdeck, that takes a vector of cards and a
indices, and returns a vector of cards that contains the specified
subdeck of the deck:

```
Deck::subdeck(int low, int high) const {
Deck sub(high-low);
```

```
for (int i = 0; i<sub.cards.length(); i++) {
sub.cards[i] = cards[low+i];
}
```

```
return sub;
}
```

To create the local variable subdeck we are using the Deck constructor
that takes the size of the deck as an argument and does not initialize the
cards. The cards are initialized when they are copied from the original deck.
The length of the deck is high-low+1 because both the low card and
high card are included. This sort of computation is confusing, and can lead
“off-by-one” errors. Drawing a picture is usually the best way to avoid them.
An exercise, write a version of findbisect that takes a subdeck as an
argument, rather than a deck and an index range. Which version is more error-\prone? Which version do you think is more efficient?