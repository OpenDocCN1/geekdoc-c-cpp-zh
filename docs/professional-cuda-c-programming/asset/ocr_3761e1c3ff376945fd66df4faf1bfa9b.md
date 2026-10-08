threads access

![](bbox=[0.147, 0.127, 0.584, 0.253])

FIGURE 5-9

threads access

![](bbox=[0.147, 0.336, 0.584, 0.462])

FIGURE 5-10

# Memory Padding

Memory padding is one way to avoid bank conflicts. A simple case: Suppose you have only five shared memory banks. If all threads access different locations in bank 0, a five-way bank conflict occurs. One way to resolve this type of bank conflict is to add a word of padding after every *N* elements, where *N* is the number of banks. This changes the mapping from words to banks, as illustrated on the right side of Figure 5-11. The words that used to all belong to bank 0 now spread across different banks because of the padding.

| Bank 0 Bank 1 Bank 2 Bank 3 Bank 4 |
|---|---|---|---|---||
| 0 | 1 | 2 | 3 | 4 |
| 0 | 1 | 2 | 3 | 4 |
| 0 | 1 | 2 | 3 | 4 |
| 0 | 1 | 2 | 3 | 4 |
| 0 | 1 | 2 | 3 | 4 |

| Bank 0 Bank 1 Bank 2 Bank 3 Bank 4 |
|---|---|---|---|---||
| 0 | 1 | 2 | 3 | 4 |
| | 0 | 1 | 2 | 3 |
| | 4 | 0 | 1 | 2 |
| | | 3 | 4 | 0 | 1 |
| | | 2 | 3 | 4 | 0 |
| | | | 1 | 2 | 3 | 4 |

FIGURE 5-11