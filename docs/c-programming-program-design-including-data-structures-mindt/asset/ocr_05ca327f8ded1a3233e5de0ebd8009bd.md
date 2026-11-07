```
```cpp
<< "cookies: $"
<< totalNumOfBoxesSold * costOfOneBox << endl; //Line 30

if (numOfVolunteers != 0)                              //Line 31
    cout << "Line 32: The average number of "
         << "boxes sold by each volunteer: "
         << totalNumOfBoxesSold / numOfVolunteers       //Line 32
         << endl;
else                                                   //Line 33
    cout << "Line 34: No input." << endl;              //Line 34

return 0;                                               //Line 35
}                                                       //Line 36
```
```

# **Sample Run:** In this sample run, the user input is shaded.

Line 14: Enter each volunteer’s name and the number of boxes sold by each volunteer, ending with -1:

```
Sara 120
Lisa 128
Cindy 359
Nicole 267
Blair 165
Abby 290
Amy 190
Megan 450
Elizabeth 280
Meridith 290
Leslie 430
Chelsea 378
-1
```

```
Line 26: The total number of boxes sold: 3347
Line 27: Enter the cost of one box: 3.50

Line 30: The total money made by selling cookies: $11714.50
Line 32: The average number of boxes sold by each volunteer: 278
```

This program works as follows. The statements in Lines 8 to 12 declare the variables used in the program. The statement in Line 14 prompts the user to enter the data ending with -1. The statements in Lines 15 and 16 initialize the variables totalNumOfBoxesSold and numOfVolunteers. The statement in Line 17 reads the first name and stores it in name. The while statement in Line 18 checks whether name is not equal to SENTINEL. (The variable name is the loop control variable.) If name is not equal to SENTINEL, the body of the while loop executes. The statement in Line 20 reads and stores the number of boxes sold by the student in the variable totalNumOfBoxesSold and the statement in Line 21 updates the value of totalNumOfBoxesSold by adding numOfBoxesSold to it. The statement in Line 22 increments the value of numOfVolunteers by 1, and the statement in Line 23 reads and stores the next name into name. The statements in Lines 20 through 23 repeat until the program reads the SENTINEL. The statement in