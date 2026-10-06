```
// Determine the result.
If found == True Then
  Set result = names[index]
Else
  Set result = "That name was not found in the array."
End If
  Return result
End Function
```

# # Programming Exercises

![](bbox=[0.125, 0.283, 0.187, 0.351])

+   1. Total Sales

Design a program that asks the user to enter a store's sales for each day of the week. The amounts will be stored in an array. Use a loop to calculate the sales for the week and display the result.

+   2. Lottery Number Generator

Design a program that generates a 7-digit lottery number. The program should have an Integer array with 7 elements. Write a loop that steps through the array, randomly generating a number in the range of 0 through 9 for each element. Use the random function that was discussed in Chapter 6.) Then write another loop that displays the contents of the array.

+   3. Rainfall Statistics

Design a program that lets the user enter the rainfall for 12 months into an array. The program should calculate and display the total rainfall for the year, the average monthly rainfall, and the months with the highest and lowest amounts.

+   4. Number Analysis Program

Design a program that asks the user to enter a series of 20 numbers. The program should store the numbers in an array and then display the following data:

+   - The lowest number in the array
- The highest number in the array
- The total of the numbers in the array
- The average of the numbers in the array

+   5. Charge Account Validation

Design a program that asks the user to enter a charge account number. The program should determine whether the number is valid by comparing it to the following list of valid charge accounts:

|5658845 5020125 7895122 8777541 8451277 1302850 |
|8010852 5552555 5050552 7828577 1205255 |
|1005231 6452331 3850285 7576551 7881200 4581002 |

These numbers should be stored in an array. Use the sequential search algorithm to locate the number entered by the user. If the number is in the array, the program should display a message indicating the number is valid. If the number is not in the array, the program should display a message indicating the number is invalid.