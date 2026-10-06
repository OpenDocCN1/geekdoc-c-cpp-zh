# 158 CHAPTER 4 Link-Based Implementations

FIGURE 4-11 (a) An array-based implementation of a linked chain; (b) after inserting "D" at the beginning of the chain; (c) after deleting "B"

| (a) | | (b) | | (c) |
| item next | | item next | | item next |
|---|---|---|---|---|---|n| 0 | B | | 0 | B | | 0 | 4 |
| 1 | E | | 1 | E | | 1 | E |
| 2 | J | -1 | | 2 | J | -1 | | 2 | J | -1 |
| 3 | 4 | | 3 | D | 0 | | 3 | D | 1 |
| 4 | 5 | | 4 | 5 | | 4 | 5 |
| 5 | 6 | | 5 | 6 | | 5 | 6 |
| 6 | 7 | | 6 | 7 | | 6 | 7 |
| ... | | | ... | | | ... | |
| ... | | | ... | | | ... | |
| | -1 | | | -1 | | | -1 |
| head | free | | head | free | | head | free |