```
```c
wDeck[i].suit = i / (CARDS / 4);
wDeck[i].color = i / (CARDS / 2);
}

// output cards in two-column format; cards 0-25 indexed with
// k1 (column 1); cards 26-51 indexed with k2 (column 2)
void deal(const Card * const wDeck)
{
printf("%-6s%-6s%-15s%-6s%-6s\n", "Card", "Suit", "Color",
"Card", "Suit", "Color");

// loop through wDeck
for (size_t k1 = 0, k2 = k1 + 26; k1 < CARDS / 2; ++k1, ++k2) {
printf("Card:%3d Suit:%2d Color:%2d ", wDeck[k1].face, wDeck[k1].suit, wDeck[k1].color);
printf("Card:%3d Suit:%2d Color:%2d\n", wDeck[k2].face, wDeck[k2].suit, wDeck[k2].color);
}
}
```
```

Fig. 10.16 | Representing cards with bit fields in a struct. (Part 2 of 2.)

Card values 0-12 correspond to Ace through King
Suit values 0-3 correspond Hearts, Diamonds, Clubs and Spades
Color values 0-1 correspond to red and black

| Card | Suit | Color | Card | Suit | Color |
|------|------|-------|------|------|-------|
| 0 | 0 | 0 | 0 | 2 | 1 |
| 1 | 0 | 0 | 1 | 2 | 1 |
| 2 | 0 | 0 | 2 | 2 | 1 |
| 3 | 0 | 0 | 3 | 2 | 1 |
| 4 | 0 | 0 | 4 | 2 | 1 |
| 5 | 0 | 0 | 5 | 2 | 1 |
| 6 | 0 | 0 | 6 | 2 | 1 |
| 7 | 0 | 0 | 7 | 2 | 1 |
| 8 | 0 | 0 | 8 | 2 | 1 |
| 9 | 0 | 0 | 9 | 2 | 1 |
| 10 | 0 | 0 | 10 | 2 | 1 |
| 11 | 0 | 0 | 11 | 2 | 1 |
| 12 | 0 | 0 | 12 | 2 | 1 |
| 0 | 1 | 0 | 0 | 3 | 1 |
| 1 | 1 | 0 | 1 | 3 | 1 |
| 2 | 1 | 0 | 2 | 3 | 1 |
| 3 | 1 | 0 | 3 | 3 | 1 |
| 4 | 1 | 0 | 4 | 3 | 1 |
| 5 | 1 | 0 | 5 | 3 | 1 |
| 6 | 1 | 0 | 6 | 3 | 1 |
| 7 | 1 | 0 | 7 | 3 | 1 |
| 8 | 1 | 0 | 8 | 3 | 1 |
| 9 | 1 | 0 | 9 | 3 | 1 |
| 10 | 1 | 0 | 10 | 3 | 1 |
| 11 | 1 | 0 | 11 | 3 | 1 |
| 12 | 1 | 0 | 12 | 3 | 1 |

Fig. 10.17 | Output of the program in Fig. 10.16.