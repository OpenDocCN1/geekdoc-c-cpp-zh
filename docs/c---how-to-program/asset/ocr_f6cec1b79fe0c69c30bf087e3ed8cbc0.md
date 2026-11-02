The preceding structure definition indicates that member face is stored in 4 bits, member suit is stored in 2 bits and member color is stored in 1 bit. The number of bits is based on the desired range of values for each structure member. Member face stores values from 0 (Ace) through 12 (King)—4 bits can store values in the range 0–15. Member suit stores values from 0 to 3 (0 = Hearts, 1 = Diamonds, 2 = Clubs, 3 = Spades)—2 bits can store values in the range 0–3. Finally, member color stores either 0 (Red) or 1 (Black)—1 bit can store either 0 or 1.

# 10.10.2 Using Bit Fields to Represent a Card's Face, Suit and Color

Figure 10.16 (output shown in Fig. 10.17) creates array deck containing 52 struct bitCard structures in line 20. Function fillDeck (lines 31–39) inserts the 52 cards in the deck array and function deal1 (lines 43–55) prints the 52 cards. Notice that bit field members of structures are accessed exactly as any other structure member. Member color is included as a means of indicating the card color on a system that allows color displays.

```
```c
1 // Fig. 10.16: fig10_16.c
2 // Representing cards with bit fields in a struct
3 #include <stdio.h>
4 #define CARDS 52
5
6 // bitCard structure definition with bit fields
7 struct bitCard {
8     unsigned int face : 4; // 4 bits; 0-15
9     unsigned int suit : 2; // 2 bits; 0-3
10    unsigned int color : 1; // 1 bit; 0-1
11 };
12
13 typedef struct bitCard Card; // new type name for struct bitCard
14
15 void fillDeck(Card * const wDeck); // prototype
16 void deal(const Card * const wDeck); // prototype
17
18 int main(void)
19 {
20     Card deck[CARDS]; // create array of Cards
21
22     fillDeck(deck);
23
24     puts("Card values 0-12 correspond to Ace through King");
25     puts("Suit values 0-3 correspond Hearts, Diamonds, Clubs and Spades");
26     puts("Color values 0-1 correspond to red and black\n");
27     deal(deck);
28 }
29
30 // initialize Cards
31 void fillDeck(Card * const wDeck)
32 {
33     // loop through wDeck
34     for (size_t i = 0; i < CARDS; ++i) {
35         wDeck[i].face = i % (CARDS / 4);
```
```