# CHAPTER 2 Beginning the Problem-Solving Process

| total charge | liquor charge | tip percentage | total bill without liquor charge | tip |
| --- | --- | --- | --- | --- |
| 45 | 10 | 15% | 35 | 5 |
| 30 | 0 | 15 | 30 | |

**Figure 2-19** Value of the second desk-check's processing item entered in the desk-check table

The third instruction in the algorithm is to calculate the value in the total bill without liquor charge (15). You record the result (4.50) in the tip percentage column, as shown in Figure 2-20. The last instruction in the algorithm is to display the tip. In this case, number 45.0 will be displayed, which agrees with the manual calculation shown in Figure 2-17.

| total bill | liquor charge | tip percentage | total bill without liquor charge | tip |
| --- | --- | --- | --- | --- |
| 45 | 10 | 15% | 35 | 5 |
| 30 | 0 | 15 | 30 | 4.50 |

**Figure 2-20** Value of the second desk-check's output item entered in the desk-check table

To be sure an algorithm works correctly, you should desk-check several times using both valid and invalid data. **Valid data** is data that the algorithm is expecting the user to enter. For example, the algorithm that you finished desk-check expects the user to provide positive numbers for the input values. **Invalid data** is data that the algorithm is not expecting the user to enter, such as a negative number for the total bill. You should test an algorithm with invalid data because users sometimes make mistakes when entering data. In later chapters in this book, you will learn how to write algorithms that correctly handle input errors. For now, you can assume that the user will always enter valid data.

# The Gas Mileage Problem

The gas mileage problem will help reinforce what you learned in this chapter. Figure 2-21 shows the problem specification.

>  Cheryl Harrison began her trip from New York to Wyoming, she filled her car's tank with gas and reset her trip meter to zero. After traveling 324 miles, Cheryl stopped at a gas station to refuel, the gas tank required 17 gallons. Cheryl wants a program that calculates and displays her car's gas mileage at any time during the trip. The gas mileage is the number of miles her car was driven per gallon of gas.

**Figure 2-21** Problem specification for the gas mileage problem