# 180 Selection Structures

code for 'C', and so on. For character sets coded in this manner, the following conditions are evaluated as shown:

| Expression | Value | Interpretation |
|---|---|---|n| 'A' > 'C' | 0 | false |
| 'D' <= 'Z' | 1 | true |
| 'E' == 'F' | 0 | false |
| 'g' != 'm' | 0 | false |
| 'b' != 'c' | 1 | true |
| 'a' == 'A' | 0 | false |
| 'B' < 'a' | 0 | true |
| 'b' > 'Z' | 1 | true |

Comparing letters is essential in alphabetizing names or using characters to select a choice in decision-making. Strings of characters can also be compared, and two string expressions can be compared by relational operators or the string class's comparison methods (discussed in Section 9.3). In the ASCII character set, a blank precedes (and is considered "less than") all letters and numbers: the letters of the alphabet are stored in order from A to Z; digits are stored in order from 0 to 9. In this sequence, lowercase letters come after (considered "greater than") uppercase letters, and letter codes come after ("greater than") digit codes (see Appendix B).
When two strings are compared, their characters are compared one pair at a time (both first characters are equal, then second characters, and so on). If no difference is found, the string with the first lower character is considered the smaller string. Following are examples of string comparisons:

| Expression | Value | Interpretation | Comment |
|---|---|---|---|n| "Hello" > "Good-bye" | 1 | true | The first H in Hello is greater than the first G in Good-bye |
| "SMITH" > " JONES" | 1 | true | The first S in SMITH is greater than the first J in JONES |
| "123" > "1227" | 1 | true | The third character in 123, the 3, is greater than the third character in 1227, the 2. |
"Behop" > "Beehive" | 1 | true | The third character in Behop, the h, is greater than the third character in Beehive, the e. |
"He" == "She" | 0 | false | The first H in He is not equal to the first S in She. |
"plant" < "planet" | 0 | false | The t in plant is greater than the e in planet. |