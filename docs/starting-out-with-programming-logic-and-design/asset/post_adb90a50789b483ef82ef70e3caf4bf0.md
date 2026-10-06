
Write a pseudocode algorithm that uses the For Each loop to display all the values in the following array:

Constant Integer SIZE = 10
Declare Integer values[SIZE] = 1, 2, 3, 4, 5, 6, 7, 8, 9, 10

## Debugging Exercises

- 1. What is the error in the following pseudocode?

```
// This program uses an array to display five names.
Constant Integer SIZE = 5
Declare String names[SIZE] = "Meg", "Jack", "Steve", "Bill", "Lisa"
Declare Integer index
For index = 0 To SIZE
  Display names[index]
End For
```

- 2. What is the error in the following pseudocode?

```
// This program displays the highest value in the array.
Constant Integer SIZE = 3
Declare Integer values[SIZE] = 1, 3, 4
Declare Integer index
Declare Integer highest
For index = 0 To SIZE - 1
  If values[index] > highest
    Set highest = values[index]
End If
```

Display "The highest number is ", highest

- 3. What is the error in the following pseudocode?

// The searchName function accepts a string containing the name
// to search, an array of strings and an integer specifying the size of the array. The function
// searches for the name in the array. If the name is found, the string containing the name is returned; otherwise a message
// indicating that the name was not found in the array is
 returned.

```
Function searchName(String name, String names[],
  Declare Boolean found
  Declare Integer index
  Declare String result
  // Step through the array searching for the
  // specified name.
  While found == False AND index <= size - 1
    If contains(names[index], name) Then
      Set found = True
    Else
      Set index = index + 1
    End If
End While

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

## Programming Exercises

![](img/c939132f78787c7f339c6977b3fc8c85_359_0.png)

- 1. Total Sales

Design a program that asks the user to enter a store's sales for each day of the week. The amounts will be stored in an array. Use a loop to calculate the sales for the week and display the result.

- 2. Lottery Number Generator

Design a program that generates a 7-digit lottery number. The program should have an Integer array with 7 elements. Write a loop that steps through the array, randomly generating a number in the range of 0 through 9 for each element. Use the random function that was discussed in Chapter 6.) Then write another loop that displays the contents of the array.

- 3. Rainfall Statistics

Design a program that lets the user enter the rainfall for 12 months into an array. The program should calculate and display the total rainfall for the year, the average monthly rainfall, and the months with the highest and lowest amounts.

- 4. Number Analysis Program

Design a program that asks the user to enter a series of 20 numbers. The program should store the numbers in an array and then display the following data:

- The lowest number in the array
- The highest number in the array
- The total of the numbers in the array
- The average of the numbers in the array

- 5. Charge Account Validation

Design a program that asks the user to enter a charge account number. The program should determine whether the number is valid by comparing it to the following list of valid charge accounts:

| 5658845 | 5020125 | 7895122 | 8777541 | 8451277 | 1302850 |
| 8010852 | 5552555 | 5050552 | 7828577 | 1205255 |
| 1005231 | 6452331 | 3850285 | 7576551 | 7881200 | 458102 |

### These numbers should be stored in an array. Use the sequential algorithm to locate the number entered by the user. If the number is in the array, the program should display a message indicating is valid. If the number is not in the array, the program should display a message indicating invalid.

- 6. Days of Each Month

Design a program that displays the number of days in each month. The program's output should be similar to:

```
January has 31 days.
February has 28 days.
March has 31 days.
April has 30 days.
May has 31 days.
June has 30 days.
July has 31 days.
August has 31 days.
September has 30 days.
October has 31 days.
November has 30 days.
December has 31 days.
```

The program should have two parallel arrays: a 12-element String array that is initialized with the names of the months, and a 12-element Integer array that is initialized with the number of days in each month. To produce the output, use a loop to step through the arrays getting a name of a month and the number of days.

- 7. Phone Number Lookup

Design a program that has two parallel arrays: a String array named people that is initialized with the names of friends, and a String array named phoneNumbers that is initialized with your phone numbers. The program should allow the user to enter a person's name (or part of a person name). It should search for that in the people array. If the person is found, it should get that person's phone number from the phoneNumbers array and display it. If the person is not in the people array, the program should display a message so.

- 8. Payroll

Design a program that uses the following parallel arrays:

- empId: An array of Integers to hold identification numbers. The array should be initialized with the following numbers: 65588, 45201, 78951, 84512, 13028, 75804
- hours: An array of Integers to hold the number of hours worked by each employee.
- payRate: An array of Reals to hold each employee's hourly rate.
- wages: An array of Reals to hold each employee's gross wages.

The program should read the data in each array through the subscripts. For example, the number in element 0 of the hours worked by the employee whose identification number is stored in element 0 of the empId array. That employee's pay rate should be stored in element 0 of the payRate array. The program should display each employee name and ask the user to enter that employee's hours and pay rate (hours times rate), which should be stored in the wages array. After the data has been entered for all the employees, the program should display each employee's identification number and gross wages.

## Driver's License Exam

The driver's license office has asked you to design a program that grades the written portion of the driver's exam. The exam has 20 multiple choice questions. Here are the correct answers:

1. B | 6. A | 11. B | 16. C
2. D | 7. B | 12. C | 17. C
3. A | 8. A | 13. D | 18. B
4. A | 9. C | 14. A | 19. D
5. C | 10. D | 15. D | 20. A

Your program should store these correct answers in an array. (Store each question's correct answer in an element of a string array.) For each of the 20 questions, which should be stored in another array. After the student's answers have been entered, the program should display a message indicating whether the student passed or failed the exam (A student must correctly answer 15 of the 20 questions to pass the exam). It should then display the total number of correctly answered questions, and a list showing the number of incorrectly answered questions.

## Tic-Tac-Toe Game

Design a program that allows two players to play a game of tic-tac-toe using a two-dimensional array with three rows and three columns as the game board. Each element of the array should be initialized with an asterisk (*). The program should run a loop that does the following:

a. Displays the contents of the board array.
b. Allows player 1 to select a location on the board for an X. The program should ask the user to enter the row and column number.
c. Allows player 2 to select a location on the board for an O. The program should ask the user to enter the row and column number.
d. Determines whether a player has won or if a tie has occurred. If a player has won, the program should display the winning player and the winner. If a tie has occurred, the program should say so and end.
e. Player 1 wins when there are three Xs in a row, three Os in a row on the game board. The winning Xs or Os can appear in a row, in a column, or diagonally across the board. A tie occurs when all of the locations on the board are full, but there is no winner.

## Lo Shu Magic Square

The Lo Shu Magic Square is a grid with 3 rows and 3 columns shown in Figure 8-23. The Lo Shu Magic Square has the following properties:

- The grid contains the numbers 1 through 9 exactly.
- The sum of each row, column, and each diagonal adds up to the same number. This is shown in Figure 8-24.

In a program, you can simulate a magic square using a two-dimensional array. Design a program that initializes a two-dimensional array with values entered by the user. The program should determine whether the array is a Lo Shu Magic Square.
