# Example 28 Some Standard Formatting Patterns and Their Effects

Formatting is culture-sensitive. This table shows the formatting in the en-US culture.

| Number | {0:D4} | {0,7} | {0:F0} | {0:F2} | {0,8:F3} | {0:E4} | {0,9:C} |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 0 | 0000 | | | 0.00 | 0.0000+E00 | | $0.00 |
| 1 | 0001 | 1 | 1.00 | 1.000 | 1.0000+E02 | | $1.00 |
| 145 | 0145 | 145 | 145.00 | 145.000 | 1.4500+E02 | | $145.00 |
| -1 | -0001 | -1 | -1.00 | -1.000 | -1.0000+E02 | | ($1.00) |
| 2.5 | | 3 | 2.50 | 2.500 | | | $2.50 |
| -1.5 | | -1.2 | -1.50 | -1.500 | | | ($1.50) |
| 330.8 | | 330. 8 | 331 | 330.80 | 3.3080+E02 | | $330.80 |
| 1234.516 | | 11234.516 | 1235 | 1234.52 | 1234.516 | 1.2345+E03 | | $1,234.56 |

# Example 29 Custom Number Formatting

| Number | {0:000.0} | {0:#..#} | {0:#.0} | {0:#E+0} | {0:;;(neg)}' | | |
| --- | --- | --- | --- | --- | --- | --- |
| 1230.1 | 1230.1 | 1230.1 | | 12E+2 | | 1230 |
| 17 | 017.0 | 17 | 17.0 | 17E+0 | | 0017 |
| 0.15 | 000.2 | | | 15E-2 | | |
| 0 | 000.0 | | 2 | 0.0 | 00E+0 | | |
| -26 | -026.0 | -26 | -26.0 | -26E+0 | | (neg) |

# Example 30 Standard DateTime Formatting and Their Effects

Here a DateTime value shown in all standard formats using the en-US culture and the de-DE culture:

| Format | U.English | German |
| --- | --- | --- |
| F | Monday, June 09, 2003 10:49:41 PM | Montag, 9. Juni 2003 22:49:41 |
| f | Monday, June 09, 2003 10:49 PM | Montag, 9. Juni 2003 22:49 |
| g | 6/9/2003 10:49:41 | 09.06.2003 22:49:41 |
| G | 6/9/2003 10:49 PM | 09.06.2003 22:49 |
| s | 2003-06-09T22:49:41Z | 2003-06-09T22:49:41Z |
| u | 2003-06-09 22:49:41Z | 2003-06-09 22:49:41Z |
| U | Monday, June 09, 2003 8:49:41 PM | Montag, 9. Juni 2003 20:49:41 |
| R | Mon, 09 Jun 2003 22:49:41 GMT | Mon, 09 Jun 20003 22:49:41 GMT |
| d | Monday, June 09, 2003 | Montag, 9. Juni 2003 |
| y | 6/9/2003 | 09.06.2003 |
| Y | June, 2003 | Juni 2003 |
| M | June 09 | 09 Juni |
| T | 10:49:41 PM | 22:49:41 |
| t | 10:49 PM | 22:49 |