# 31. b

**Explanation**: The redefinition of preprocessor directives is allowed, the value will get substituted by the latest preprocessor directive.

# 32. d

**Explanation**: We discussed a similar concept in the explanation of question 57, group 2. 2D array is a collection of 1D arrays, Each string stored in the form of a 1D array. The base address of each 1D array cannot be modified. If we declare 2D array as *str[4], → char *str[4]="hello", "India", "love", "great";, the program will give output "hello India great love".

# 33. d

**Explanation**: We have already discussed these kinds of questions. Explanation is not required.

# 34. <blank space> ndia dia ia a

**Explanation**: A practice question, explanation not required.

# 35. a

Explanation:

| | hello | India | love | great |
|---|---|---|---|---|
| | 1000 | 2000 | 3000 | 4000 |
| Initialization: [ ] = "hello", "India", "love", "great"; | | | | |
| s | 1000 | 2000 | 3000 | 4000 |
| | 500 | 504 | 508 | 512 |
| ptr = [s+3, s+2, s+1]; | | | | |
| p - ptr; | | 500 |
| ptr | 512 | 508 | 504 | 500 |
| | 700 | 704 | 706 | 712 |

> (i) **ptr → it is
incrementing the p by 4 step
(ii) **ptr → ptr + 3**
(iii) **ptr → ptr +3**
(iv) **ptr → +500**
/character, step size is 1
(v) **ptr → +100**
will print from
address 1003 till the null character

# 36. c

Explanation:

| | 5 | 6 | 7 | 8 | 9 |
|---|---|---|---|---|---|
| | 500 | 504 | 508 | 512 | 516 |
| Initialization:
x[]=[5,6,7,8,9];
*p[] = [x,x+1,x+2,x+3,x+4];
**ptr - p; | p | 500 | 504 | 508 | 512 | 516 |
| | 1000 | 1004 | 1008 | 1012 | 1016 |
| ptr | 1004 | |
| | 2000 |

> (i) **ptr++**;
(ii) **ptr → 1004 → 4**; This is a ptr
(iii). We know the integer size is 4B,
For 4, the %d format specifier returns 1.
If it is, it returns.
(iv) **ptr → 504 → 4**; 1 will be printed.
Reason: same as above
(v) **ptr → **1004 → 6**;

# 37. a