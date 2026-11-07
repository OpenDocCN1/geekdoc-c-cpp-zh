| St. | Execution of the Statement | Effect |
|---|---|---|
| 2 | `cin >> calBurnedInOneDay;` | `calBurnedInOneDay = 375` |
| 3 | `calBurnedInAWeek = calBurnedInAWeek + calBurnedInOneDay;` | `calBurnedInAWeek = 0 + 375 = 375` |
| 2 | `cin >> calBurnedInOneDay;` | `calBurnedInOneDay = 425` |
| 3 | `calBurnedInAWeek = calBurnedInAWeek + calBurnedInOneDay;` | `calBurnedInAWeek = 375 + 425 = 800` |
| 2 | `cin >> calBurnedInOneDay;` | `calBurnedInOneDay = 270` |
| 3 | `calBurnedInAWeek = calBurnedInAWeek + calBurnedInOneDay;` | `calBurnedInAWeek = 800 + 270 = 1070` |

From this table it is clear that after executing statements 2 and 3 three times, calBurnedInAWeek contains the sum of the calories burned in the first three days. If we execute these two statements seven times, then calBurnedInAWeek contains the sum of the calories burned in a week.

If you want to find the calories burned in 30 days, then you can repeat statements 2 and 3 fifty times, and if you want to find the calories burned in 100 days, you can repeat statements 2 and 3 one hundred times. In either case, you do not have to declare any additional variables, as you did in the previous C++ program. However, as it is written now, we would have to rewrite statements 2 and 3 for each value of calBurnedInOneDay we want to add to calBurnedInAWeek. We need a structure that will tell the computer to repeat these same 2 statements 7 times, or 30 times, or 100 times, however many repetitions we want. Then we can use this C++ code to add any number of values, whereas the earlier code adds a specific number of values and requires you to drastically change the code to change the number of values.

There are many other situations in which it is necessary to repeat a set of statements. For example, for each student in a class, the formula for determining the course grade is the same. C++ has three repetition, or looping, structures that let you repeat statements over and over until certain conditions are met. This chapter introduces all three looping (repetition) structures. The next section discusses the first repetition structure, called the while loop.