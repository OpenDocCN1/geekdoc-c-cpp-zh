```
```c
// shuffle cards in deck
void shuffle(unsigned int wDeck[][FACES])
{
    // for each of the cards, choose slot of deck randomly
    for (size_t card = 1; card <= CARDS; ++card) {
        size_t row; // row number
        size_t column; // column number

        // choose new random location until unoccupied slot found
        do {
            row = rand() % SUITS;
            column = rand() % FACES;
        } while(wDeck[row][column] != 0);

        // place card number in chosen slot of deck
        wDeck[row][column] = card;
    }
}

// deal cards in deck
void deal(const unsigned int wDeck[][FACES], const char *wFace[],
          const char *wSuit[])
{
    // deal each of the cards
    for (size_t card = 1; card <= CARDS; ++card) {
        // loop through rows of wDeck
        for (size_t row = 0; row < SUITS; ++row) {
            // loop through columns of wDeck for current row
            for (size_t column = 0; column < FACES; ++column) {
                // if slot contains current card, display card
                if (wDeck[row][column] == card) {
                    printf("%5s of %-8s", wFace[column], wSuit[row],
                           card % 2 == 0 ? '\n' : '\t'); // 2-column format
                }
            }
        }
    }
}
```
```

Fig. 7.24 | Card shuffling and dealing. (Part 2 of 2.)

|  |  |
|---|---|
| Nine of Hearts | Five of Clubs |
| Queen of Spades | Three of Spades |
| Queen of Hearts | Ace of Clubs |
| King of Hearts | Six of Spades |
| Jack of Diamonds | Five of Spades |
| Seven of Hearts | King of Clubs |
| Three of Clubs | Eight of Hearts |
| Three of Diamonds | Four of Diamonds |
| Queen of Diamonds | Five of Diamonds |

Fig. 7.25 | Sample run of card dealing program. (Part I of 2.)