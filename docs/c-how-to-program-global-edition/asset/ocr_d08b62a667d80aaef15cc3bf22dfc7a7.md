![](bbox=[0.18, 0.12, 0.82, 0.38])

Fig. 7.23 | Two-dimensional array representation of a deck of cards.

# Possibility of Indefinite Postponement

This shuffling algorithm can execute indefinitely if cards that have already been shuffled are repeatedly selected at random. This phenomenon is known as indefinite postponement. In this chapter's exercises, we discuss a better shuffling algorithm that eliminates the possibility of indefinite postponement.

> Performance Tip 7.3
> Sometimes an algorithm that emerges in a "natural" way can contain subtle performance problems, such as indefinite postponement. Seek algorithms that avoid indefinite postponement.

# Dealing Cards from the Two-Dimensional Array

To deal the first card, we search the array for deck[row][column] equal to 1. This is accomplished with nested for statements that vary row from 0 to 3 and column from 0 to 12. What card does that element of the array correspond to? The suit array has been preloaded with the four suits, so to get the suit, we print the character string suit[row]. Similarly, to get the face value of the card, we print the character string face[column]. We also print the character string " of ". Printing this information in the proper order enables us to print each card in the form "King of Clubs", "Ace of Diamonds" and so on.

# Developing the Program's Logic with Top-Down, Stepwise Refinement

Let's proceed with the top-down, stepwise refinement process. The top is simply

Shuffle and deal 52 cards

Our first refinement yields:

+   - Initialize the suit array
+   - Initialize the face array
+   - Initialize the deck array
+   - Shuffle the deck
+   - Deal 52 cards