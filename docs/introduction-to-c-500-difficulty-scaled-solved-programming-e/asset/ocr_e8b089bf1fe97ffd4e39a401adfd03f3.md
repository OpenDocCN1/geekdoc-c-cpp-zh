# 322 Introduction to C++

```
const int ROWS = 4;
const int COLS = 4;
```

```
void show_board(const int c[] [COLS], const int s[] [COLS]);
void sel_card(const int c[] [COLS], const int s[] [COLS], int row, int col);
```

```
int main() {
    int i, j, m, r, c2, cnt, cnt, cards [ROWS], status [ROWS] [COLS]
    = {0}; /* The status array indicates if a card faces up or down (0 is for
down). */
n    cnt = 0; // This variable counts the number of the faced up cards.
    for(i = r = 0; i < ROWS; i++) // Assign the values 1 to 8,
sequentially.*/ {
        for(j = 0; j < COLS; j+=2) {
            cards[i] [j] = cards[i] [j+1] = r+1;
        }
    }
    /* Now, shuffle the cards, so that they are placed in random
positions (NULL); */
    srand(time(NULL));
    for(i = 0; i < ROWS; i++) {
        for(j = 0; j < COLS; j++) {
            c = cards[i] [j];
            m = rand() % ROWS;
            r = rand() % COLS;
            cards[i] [j] = cards[m] [r];
            cards[m] [r] = c;
        }
    }
    show_board(cards, status);
    m = 0;
    while (cnt != ROWS+COLS) /* The game ends when all cards are faced up. */ {
        sel_card(cards, status, &r, &c);
        cout << "Card_1 = " << cards[r] [c] << "\n";
        sel_card(cards, status, &r2, &c2);
        cout << "Card_2 = " << cards[r2] [c2] << "\n";
    }
    for(i = 0; i < 18; i++) /* Insert line to delete history
and make harder for the player to remember the card positions. */
        cout << "\n";
    }
    if(cards[r] [c] == cards[r2] [c2]) {
        cout << "Cards matched !!!\n";
        cnt += 2;
    }
```