# CHAPTER 5 The Selection Structure

| Input | Processing | Output |
|---|---|--|
| total calories | Processing items: none | fat calories |
| grams of fat | | fat percentage (decimal places) |

```
Algorithm:
1. enter the total calories and grams of fat
2. if (both the calories and grams of fat are greater than or equal to zero)
   calculate fat calories by multiplying grams of fat by 9
   calculate fat percentage by dividing fat calories by total calories and then multiplying the result by 100
   display the fat calories and percentage
else
   display an error message
if
```

**Figure 5-29** Completed IPO chart for the health club problem

After completing the IPO chart, you then move to the third step in the problem-solving process, you will desk-desk the algorithm. For the first desk-desk, you will desk-desk the health club algorithm three times. You will use 150 as the total calories and 6 as the grams of fat; the fat calories and fat percentage will be 54 and 36%, respectively. For the second desk-desk, you will use 105 as the total calories and 2 as the grams of fat. Using this data, the fat calories and fat percentage should be 18 and 17%, respectively. For the third desk-desk, you will use 100 as the total calories and -3 as the grams of fat. Using this data, the program should display an error message. Figure 5-30 shows the completed desk-desk table. Notice that the amounts in the fat calories and fat percentage columns agree with the results of your manual calculations.

| total calories | grams of fat | fat calories | fat percentage |
|---|---|---|--|
| 150 | 6 | 54 | 30 |
| 105 | 2 | 18 | 17 |
| 100 | -3 | | |

**Figure 5-30** Completed desk-desk table for the health club algorithm

The fourth step in the problem-solving process is to code the algorithm into a program. You begin by declaring memory locations that store the values of the input, (if any), and output items. The health club will need four memory locations to store the input and output items. The input items (total calories and grams of fat) will be stored in variables, because the user should be allowed to change the value of items during runtime. The output items (fat calories and fat percentage) also will be stored in variables, because their values are based on the current values of inputs. The total calories, grams of fat, and fat calories will