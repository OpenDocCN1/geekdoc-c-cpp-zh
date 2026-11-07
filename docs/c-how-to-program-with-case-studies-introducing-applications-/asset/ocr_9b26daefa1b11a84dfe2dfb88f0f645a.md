# Shuffling the Two-Dimensional Array

This simulated deck of cards may be shuffled as follows. First, set all elements of deck to 0. Then, choose a row (0–3) and a column (0–12) at random. Place the number 1 in array element `deck[row][column]` to indicate that this card will be the first one dealt from the shuffled deck. Repeat this process for the numbers 2, 3, …, 52, randomly inserting each in the deck array to indicate which cards are to be dealt second, third, …, and fifty-second in the shuffled deck. As the deck array begins to fill with card numbers, a card may be selected again—i.e., `deck[row][column]` will be nonzero when it’s selected. Ignore this selection and choose another random row and column values repeatedly until you find an unselected card. Eventually, the numbers 1 through 52 will occupy the deck array’s 52 slots. At that point, the deck of cards is fully shuffled.

# Possibility of Indefinite Postponement

This shuffling algorithm can execute indefinitely if cards that have already been shuffled are repeatedly selected at random. This phenomenon is known as indefinite postponement. In this chapter’s exercises, we discuss a better shuffling algorithm that eliminates the possibility of indefinite postponement.

PERF

Sometimes an algorithm that emerges in a “natural” way can contain subtle performance problems, such as indefinite postponement. Seek algorithms that avoid indefinite postponement.

# Dealing Cards from the Two-Dimensional Array

To deal the first card, we search the array for `deck[row][column]` equal to 1 using nested for statements that vary row from 0 to 3 and column from 0 to 12. What card does that element of the array correspond to? The suit array has been preloaded with the four suits, so to get the card’s suit, we print the character string `suit[row]`. Similarly, to get the card’s face, we print the character string `face[column]`. We also print the character string " of ", as in "King of Clubs", "Ace of Diamonds" and so on.

# Developing the Program’s Logic with Top-Down, Stepwise Refinement

Let’s proceed with the top-down, stepwise refinement process. The top is simply:

+   - Shuffle and deal 52 cards

Our first refinement yields:

+   - Initialize the suit array
+   - Initialize the face array
+   - Initialize the deck array
+   - Shuffle the deck
+   - Deal 52 cards

“Shuffle the deck” may be refined as follows:

+   - For each of the 52 cards
+     - Place card number in a randomly selected unoccupied element of deck