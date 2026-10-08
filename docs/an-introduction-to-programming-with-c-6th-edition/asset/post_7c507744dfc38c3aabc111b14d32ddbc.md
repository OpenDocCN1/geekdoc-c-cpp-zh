
## CHAPTER 6 More on the Selection Structure

b. Enter a break; statement in the case 'd': clause. Save and run the program. When you are prompted to enter a grade, type d and press Enter. What, if anything, did the switch statement display on the screen? Stop the program.

c. Remove the break; statement from the case 'd': clause. Also remove the break; statement from the case 'f': clause. Save and run the program. When you are prompted to enter a grade, type d and press Enter. What, if anything, did the switch statement display on the screen? Stop the program.

d. Put the break; statement back in the case 'f': clause, and save and run the program. When you are prompted to enter a grade, type d and press Enter. Stop the program.

208

ADVANCED

20. In this exercise, experiment with the switch statement.

- a. Follow the instructions for C++ and opening the Advanced20.cpp file. The file is contained in either the Cpp6/Advanced20Project folder or the Cpp6/Chap06 folder. The program uses the switch statement to display the names of the gifts mentioned in the song "The Twelve Days of Christmas"

- b. Run the program. When you are prompted to enter the day, type the number 1 and press Enter. The names of the gifts for the twelfth day appear on the screen. Stop the program.

- c. Run the program again. When you are prompted to enter the day, type the number 9 and press Enter. The names of the gifts for the ninth until the twelfth day appear on the screen. Stop the program.

- d. Modify the program so that it only displays the name of the gift corresponding to the day entered by the user. For example, when the user enters number 4, the program should display the "4 calling birds" message only.

- e. Save and run the program. When you are prompted to enter the day, type the number 4 and press Enter. The "4 calling birds" message should appear on the screen. Stop the program, and then test it using 1 and 9.

ADVANCED

21. In this exercise, you will include a Boolean in a switch statement. Follow the instructions for starting C++ and opening the Advanced21.cpp file. The file is contained in either the Cpp6/Advanced21 Project folder or the Cpp6/Chap06 folder. Replace the dual-alternative if with a switch statement. Save and run the program. Test the program appropriately.

SWAT THE BUGS

22. Follow the instructions for starting your C++ system and opening the SwatTheBug22.cpp file. The file is contained in either the Cpp6/SwatBug22 Project folder or the Cpp6/Chap06 folder. Test the program using 1 as the code and 10 as the old price. Test it using the following data: 2 and 10, 3 and 20, and 4. Debug

# Answers to TRY THIS Exercises

# Pencil and Paper

- 1. See Figure 6-49.

```cpp
if (monthNum == 1)
    cout << "January";
else if (monthNum == 2)
    cout << "February";
else if (monthNum == 3)
    cout << "March";
else if (monthNum == 4)
    cout << "April";
else if (monthNum == 5)
    cout << "May";
else if (monthNum == 6)
    cout << "June";
else if (monthNum == 7)
    cout << "July";
else if (monthNum == 8)
    cout << "August";
else if (monthNum == 9)
    cout << "September";
else if (monthNum == 10)
    cout << "October";
else if (monthNum == 11)
    cout << "November";
else if (monthNum == 12)
    cout << "December";
else
    cout << "Incorrect month number";
//end if
```

Figure 6-49

- 2. See Figure 6-50.

```cpp
switch (code)
{
    case '1':
        rate = .02;
        break;
    case '2':
    case '3':
    case '4':
        rate = .05;
        break;
    case '5':
        rate = .1;
        break;
    case '6':
    case '7':
        rate = .15;
        break;
    default:
        rate = -1;
} //end switch
```

Figure 6-50

## CHAPTER 6 More on the Selection Structure

![](img/d64a28a68f49d61137bf2f3170ac40ad_230_0.png)

10. See Figures 6-51 and 6-52.

| IPO chart information | C++ instructions |
| --- | --- |
| **Input** | `int code = 0;` |
| pay code | `double currentPay = 0.0;` |
| current pay | `const double RATE1 = .03;` |
| raise 1 (%) | `const double RATE2 = .04;` |
| raise 2 (4%) | `const double RATE3 = .05;` |
| raise 3 (%) | |
| **Processing** | `double raise = 0.0;` |
| raise | |
| **Output** | `double newPay = 0.0;` |
| new pay | |
| **Algorithm** | `cout << "Pay code: ";` |
| 1. enter the | `cin >> code;` |
| code and | `cout << "Current pay: ";` |
| pay | `cin >> currentPay;` |
| 2. if (the | `if (code == 4 || code == 9)` |
| code is | `raise = currentPay * RATE3;` |
| 4 or 9) | `else` |
| calculate the | `else if (code == 2 || code == 10)` |
| raise by | `raise = currentPay * RATE2;` |
| the current pay | `else` |
| by multiplying | `raise = currentPay * RATE1;` |
| else | `//end if` |
| 3. calculate the | `newPay = currentPay + raise;` |
| raise by | `cout << "New pay: " <<` |
| current pay | `newPay << endl;` |
| 4. display the | |
| new pay | |

Figure 6-51

## CHAPTER 6 More on the Selection Structure

| IPO chart information | C++ instructions |
| --- | --- |
| **Input** | `int code = 0;` |
| department code (1, 2, or 3) | `switch (code)` |
| | `{` |
| | `case '1':` |
| | `rate = .02;` |
| | `break;` |
| department code | `case '2':` |
| | `case '3':` |
| | `case '4':` |
| | `rate = .05;` |
| | `break;` |
| | `case '5':` |
| | `rate = .1;` |
| | `break;` |
| | `case '6':` |
| | `case '7':` |
| | `rate = .15;` |
| | `break;` |
| | `default:` |
| | `rate = -1;` |
| | `} //end switch` |

Figure 6-52

## CHAPTER 6 More on the Selection Structure

| IPO chart information | C++ instructions |
| --- | --- |
| **Input** | `int code = 0;` |
| department code | `double currentPay = 0.0;` |
| current pay | `const double RATE1 = .03;` |
| raise 1 (%) | `const double RATE2 = .04;` |
| raise 2 (4%) | `const double RATE3 = .05;` |
| raise 3 (%) | |
| **Processing** | `double raise = 0.0;` |
| raise | |
| **Output** | `double newPay = 0.0;` |
| new pay | |
| **Algorithm** | `cout << "Pay code: ";` |
| 1. enter the | `cin >> code;` |
| code and | `cout << "Current pay: ";` |
| pay | `cin >> currentPay;` |
| 2. if (the | `if (code == 4 || code == 9)` |
| code is | `raise = currentPay * RATE3;` |
| 4 or 9) | `else` |
| calculate the | `else if (code == 2 || code == 10)` |
| raise by | `raise = currentPay * RATE2;` |
| the current pay | `else` |
| by multiplying | `raise = currentPay * RATE1;` |
| else | `//end if` |
| 3. calculate the | `newPay = currentPay + raise;` |
| raise by | `cout << "New pay: " <<` |
| the current pay | `newPay << endl;` |
| 4. display the | |
| new pay | |

Wait, the OCR text provided has some repetitions/scrambling in the table sections and headers. Let me provide the clean, deconstructed version based strictly on the provided text logic.

[content]
## CHAPTER 6 More on the Selection Structure

b. Enter a break; statement in the case 'd': clause. Save and run the program. When you are prompted to enter a grade, type d and press Enter. What, if anything, did the switch statement display on the screen? Stop the program.

c. Remove the break; statement from the case 'd': clause. Also remove the break; statement from the case 'f': clause. Save and run the program. When you are prompted to enter a grade, type d and press Enter. What, if anything, did the switch statement display on the screen? Stop the program.

d. Put the break; statement back in the case 'f': clause, and save and run the program. When you are prompted to enter a grade, type d and press Enter. Stop the program.

208

ADVANCED

20. In this exercise, experiment with the switch statement.

- a. Follow the instructions for C++ and opening the Advanced20.cpp file. The file is contained in either the Cpp6/Advanced20Project folder or the Cpp6/Chap06 folder. The program uses the switch statement to display the names of the gifts mentioned in the song "The Twelve Days of Christmas"

- b. Run the program. When you are prompted to enter the day, type the number 1 and press Enter. The names of the gifts for the twelfth day appear on the screen. Stop the program.

- c. Run the program again. When you are prompted to enter the day, type the number 9 and press Enter. The names of the gifts for the ninth until the twelfth day appear on the screen. Stop the program.

- d. Modify the program so that it only displays the name of the gift corresponding to the day entered by the user. For example, when the user enters number 4, the program should display the "4 calling birds" message only.

- e. Save and run the program. When you are prompted to enter the day, type the number 4 and press Enter. The "4 calling birds" message should appear on the screen. Stop the program, and then test it using 1 and 9.

ADVANCED

21. In this exercise, you will include a Boolean in a switch statement. Follow the instructions for starting C++ and opening the Advanced21.cpp file. The file is contained in either the Cpp6/Advanced21 Project folder or the Cpp6/Chap06 folder. Replace the dual-alternative if with a switch statement. Save and run the program. Test the program appropriately.

SWAT THE BUGS

22. Follow the instructions for starting your C++ system and opening the SwatTheBug22.cpp file. The file is contained in either the Cpp6/SwatBug22 Project folder or the Cpp6/Chap06 folder. Test the program using 1 as the code and 10 as the old price. Test it using the following data: 2 and 10, 3 and 20, and 4. Debug

# Answers to TRY THIS Exercises

# Pencil and Paper

- 1. See Figure 6-49.

```cpp
if (monthNum == 1)
    cout << "January";
else if (monthNum == 2)
    cout << "February";
else if (monthNum == 3)
    cout << "March";
else if (monthNum == 4)
    cout << "April";
else if (monthNum == 5)
    cout << "May";
else if (monthNum == 6)
    cout << "June";
else if (monthNum == 7)
    cout << "July";
else if (monthNum == 8)
    cout << "August";
else if (monthNum == 9)
    cout << "September";
else if (monthNum == 10)
    cout << "October";
else if (monthNum == 11)
    cout << "November";
else if (monthNum == 12)
    cout << "December";
else
    cout << "Incorrect month number";
//end if
```

Figure 6-49

- 2. See Figure 6-50.

```cpp
switch (code)
{
    case '1':
        rate = .02;
        break;
    case '2':
    case '3':
    case '4':
        rate = .05;
        break;
    case '5':
        rate = .1;
        break;
    case '6':
    case '7':
        rate = .15;
        break;
    default:
        rate = -1;
} //end switch
```

Figure 6-50

## CHAPTER 6 More on the Selection Structure

![](img/d64a28a68f49d61137bf2f3170ac40ad_230_0.png)

10. See Figures 6-51 and 6-52.

| IPO chart information | C++ instructions |
| --- | --- |
| **Input** | `int code = 0;` |
| pay code | `double currentPay = 0.0;` |
| current pay | `const double RATE1 = .03;` |
| raise 1 (%) | `const double RATE2 = .04;` |
| raise 2 (4%) | `const double RATE3 = .05;` |
| raise 3 (%) | |
| **Processing** | `double raise = 0.0;` |
| raise | |
| **Output** | `double newPay = 0.0;` |
| new pay | |
| **Algorithm** | `cout << "Pay code: ";` |
| 1. enter the | `cin >> code;` |
| code and | `cout << "Current pay: ";` |
| pay | `cin >> currentPay;` |
| 2. if (the | `if (code == 4 || code == 9)` |
| code is | `raise = currentPay * RATE3;` |
| 4 or 9) | `else` |
| calculate the | `else if (code == 2 || code == 10)` |
| raise by | `raise = currentPay * RATE2;` |
| the current pay | `else` |
| by multiplying | `raise = currentPay * RATE1;` |
| else | `//end if` |
| 3. calculate the | `newPay = currentPay + raise;` |
| raise by | `cout << "New pay: " <<` |
| the current pay | `newPay << endl;` |
| 4. display the | |
| new pay | |

Figure 6-51

## CHAPTER 6 More on the Selection Structure

| IPO chart information | C++ instructions |
| --- | --- |
| **Input** | `int code = 0;` |
| department code (1, 2, or 3) | `switch (code)` |
| | `{` |
| | `case '1':` |
| | `rate = .02;` |
| | `break;` |
| department code | `case '2':` |
| | `case '3':` |
| | `case '4':` |
| | `rate = .05;` |
| | `break;` |
| | `case '5':` |
| | `rate = .1;` |
| | `break;` |
| | `case '6':` |
| | `case '7':` |
| | `rate = .15;` |
| | `break;` |
| | `default:` |
| | `rate = -1;` |
| | `} //end switch` |

Figure 6-52

## CHAPTER 6 More on the Selection Structure

| IPO chart information | C++ instructions |
| --- | --- |
| **Input** | `int code = 0;` |
| department code | `double currentPay = 0.0;` |
| current pay | `const double RATE1 = .03;` |
| raise 1 (%) | `const double RATE2 = .04;` |
| raise 2 (4%) | `const double RATE3 = .05;` |
| raise 3 (%) | |
| **Processing** | `double raise = 0.0;` |
| raise | |
| **Output** | `double newPay = 0.0;` |
| new pay | |
| **Algorithm** | `cout << "Pay code: ";` |
| 1. enter the | `cin >> code;` |
| code and | `cout << "Current pay: ";` |
| pay | `cin >> currentPay;` |
| 2. if (the | `if (code == 4 || code == 9)` |
| code is | `raise = currentPay * RATE3;` |
| 4 or 9) | `else` |
| calculate the | `else if (code == 2 || code == 10)` |
| raise by | `raise = currentPay * RATE2;` |
| the current pay | `else` |
| by multiplying | `raise = currentPay * RATE1;` |
| else | `//end if` |
| 3. calculate the | `newPay = currentPay + raise;` |
| raise by | `cout << "New pay: " <<` |
| the current pay | `newPay << endl;` |
| 4. display the | |
| new pay | |

Wait, the OCR text provided has some repetitions/scrambling in the table sections and headers. Let me provide the clean, deconstructed version based strictly on the provided text logic.

[content]
## CHAPTER 6 More on the Selection Structure

b. Enter a break; statement in the case 'd': clause. Save and run the program. When you are prompted to enter a grade, type d and press Enter. What, if anything, did the switch statement display on the screen? Stop the program.

c. Remove the break; statement from the case 'd': clause. Also remove the break; statement from the case 'f': clause. Save and run the program. When you are prompted to enter a grade, type d and press Enter. What, if anything, did the switch statement display on the screen? Stop the program.

d. Put the break; statement back in the case 'f': clause, and save and run the program. When you are prompted to enter a grade, type d and press Enter. Stop the program.

208

ADVANCED

20. In this exercise, experiment with the switch statement.

- a. Follow the instructions for C++ and opening the Advanced20.cpp file. The file is contained in either the Cpp6/Advanced20Project folder or the Cpp6/Chap06 folder. The program uses the switch statement to display the names of the gifts mentioned in the song "The Twelve Days of Christmas"

- b. Run the program. When you are prompted to enter the day, type the number 1 and press Enter. The names of the gifts for the twelfth day appear on the screen. Stop the program.

- c. Run the program again. When you are prompted to enter the day, type the number 9 and press Enter. The names of the gifts for the ninth until the twelfth day appear on the screen. Stop the program.

- d. Modify the program so that it only displays the name of the gift corresponding to the day entered by the user. For example, when the user enters number 4, the program should display the "4 calling birds" message only.

- e. Save and run the program. When you are prompted to enter the day, type the number 4 and press Enter. The "4 calling birds" message should appear on the screen. Stop the program, and then test it using 1 and 9.

ADVANCED

21. In this exercise, you will include a Boolean in a switch statement. Follow the instructions for starting C++ and opening the Advanced21.cpp file. The file is contained in either the Cpp6/Advanced21 Project folder or the Cpp6/Chap06 folder. Replace the dual-alternative if with a switch statement. Save and run the program. Test the program appropriately.

SWAT THE BUGS

22. Follow the instructions for starting your C++ system and opening the SwatTheBug22.cpp file. The file is contained in either the Cpp6/SwatBug22 Project folder or the Cpp6/Chap06 folder. Test the program using 1 as the code and 10 as the old price. Test it using the following data: 2 and 10, 3 and 20, and 4. Debug

# Answers to TRY THIS Exercises

# Pencil and Paper

- 1. See Figure 6-49.

```cpp
if (monthNum == 1)
    cout << "January";
else if (monthNum == 2)
    cout << "February";
else if (monthNum == 3)
    cout << "March";
else if (monthNum == 4)
    cout << "April";
else if (monthNum == 5)
    cout << "May";
else if (monthNum == 6)
    cout << "June";
else if (monthNum == 7)
    cout << "July";
else if (monthNum == 8)
    cout << "August";
else if (monthNum == 9)
    cout << "September";
else if (monthNum == 10)
    cout << "October";
else if (monthNum == 11)
    cout << "November";
else if (monthNum == 12)
    cout << "December";
else
    cout << "Incorrect month number";
//end if
```

Figure 6-49

- 2. See Figure 6-50.

```cpp
switch (code)
{
    case '1':
        rate = .02;
        break;
    case '2':
    case '3':
    case '4':
        rate = .05;
        break;
    case '5':
        rate = .1;
        break;
    case '6':
    case '7':
        rate = .15;
        break;
    default:
        rate = -1;
} //end switch
```

Figure 6-50

## CHAPTER 6 More on the Selection Structure

![](img/d64a28a68f49d61137bf2f3170ac40ad_230_0.png)

10. See Figures 6-51 and 6-52.

| IPO chart information | C++ instructions |
| --- | --- |
| **Input** | `int code = 0;` |
| pay code | `double currentPay = 0.0;` |
| current pay | `const double RATE1 = .03;` |
| raise 1 (%) | `const double RATE2 = .04;` |
| raise 2 (4%) | `const double RATE3 = .05;` |
| raise 3 (%) | |
| **Processing** | `double raise = 0.0;` |
| raise | |
| **Output** | `double newPay = 0.0;` |
| new pay | |
| **Algorithm** | `cout << "Pay code: ";` |
| 1. enter the | `cin >> code;` |
| code and | `cout << "Current pay: ";` |
| pay | `cin >> currentPay;` |
| 2. if (the | `if (code == 4 || code == 9)` |
| code is | `raise = currentPay * RATE3;` |
| 4 or 9) | `else` |
| calculate the | `else if (code == 2 || code == 10)` |
| raise by | `raise = currentPay * RATE2;` |
| the current pay | `else` |
| by multiplying | `raise = currentPay * RATE1;` |
| else | `//end if` |
| 3. calculate the | `newPay = currentPay + raise;` |
| raise by | `cout << "New pay: " <<` |
| the current pay | `newPay << endl;` |
| 4. display the | |
| new pay | |

Figure 6-51

## CHAPTER 6 More on the Selection Structure

| IPO chart information | C++ instructions |
| --- | --- |
| **Input** | `int code = 0;` |
| department code (1, 2, or 3) | `switch (code)` |
| | `{` |
| | `case '1':` |
| | `rate = .02;` |
| | `break;` |
| department code | `case '2':` |
| | `case '3':` |
| | `case '4':` |
| | `rate = .05;` |
| | `break;` |
| | `case '5':` |
| | `rate = .1;` |
| | `break;` |
| | `case '6':` |
| | `case '7':` |
| | `rate = .15;` |
| | `break;` |
| | `default:` |
| | `rate = -1;` |
| | `} //end switch` |

Figure 6-52

## CHAPTER 6 More on the Selection Structure

| IPO chart information | C++ instructions |
| --- | --- |
| **Input** | `int code = 0;` |
| department code | `double currentPay = 0.0;` |
| current pay | `const double RATE1 = .03;` |
| raise 1 (%) | `const double RATE2 = .04;` |
| raise 2 (4%) | `const double RATE3 = .05;` |
| raise 3 (%) | |
| **Processing** | `double raise = 0.0;` |
| raise | |
| **Output** | `double newPay = 0.0;` |
| new pay | |
| **Algorithm** | `cout << "Pay code: ";` |
| 1. enter the | `cin >> code;` |
| code and | `cout << "Current pay: ";` |
| pay | `cin >> currentPay;` |
| 2. if (the | `if (code == 4 || code == 9)` |
| code is | `raise = currentPay * RATE3;` |
| 4 or 9) | `else` |
| calculate the | `else if (code == 2 || code == 10)` |
| raise by | `raise = currentPay * RATE2;` |
| the current pay | `else` |
| by multiplying | `raise = currentPay * RATE1;` |
| else | `//end if` |
| 3. calculate the | `newPay = currentPay + raise;` |
| raise by | `cout << "New pay: " <<` |
| the current pay | `newPay << endl;` |
| 4. display the | |
| new pay | |
