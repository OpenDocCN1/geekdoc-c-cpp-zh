
plus money equal to 1% of the money you save after paying taxes and buying clothes, other accessories, and school supplies.

- c. If you spend more than 25% of your net income to buy savings bonds, your parents spend $0.40 for each dollar you spend to buy savings bonds, plus money equal to 2% of the money you save after paying taxes and buying clothes, other accessories, and school supplies.

- 12. A bank in your town updates its customers' accounts at the end of each month. The bank offers two types of accounts: savings and checking. Every customer must maintain a minimum balance. If a customer's balance falls below the minimum balance, there is a service charge of $10.00 for savings accounts and $25.00 for checking accounts. If the balance at the end of the month is at least the minimum balance, the account receives interest as follows:

  - a. Savings accounts receive 4% interest.

  - b. Checking accounts with balances of up to $5,000 more than the minimum balance receive 3% interest; otherwise, the interest is 5%.

Write a program that reads a customer's account number (int type), account type (char; s for savings, c for checking), minimum balance that the account should maintain, and current balance. The program should then output the account number, account type, current balance, and an appropriate message. Test your program by running it five times, using the following data:

```
46728 S 1000 2700
87324 C 1500 7689
79873 S 1000 800
89832 C 2000 3000
98322 C 1000 750
```

- 13. Write a program that implements the algorithm given in Example 1-3 (Chapter 1), which determines the monthly wages of a salesperson.

- 14. The number of lines that can be printed on a paper depends on the paper size, the point size of each character in a line, whether lines are double-spaced or single-spaced, the top and bottom margin, and the left and right margins of the paper. Assume that all characters are of the same point size, and all lines are either single-spaced or double-spaced. Note that 1 inch = 72 points. Moreover, assume that the lines are printed along the width of the paper. For example, if the length of the paper is 11 inches and width is 8.5 inches, then the maximum length of a line is 8.5 inches. Write a program that calculates the number of characters in a line and the number of lines that can be printed on a paper based on the following input from the user:

  - a. The length and width, in inches, of the paper

  - b. The top, bottom, left, and right margins

  - c. The point size of a line

  - d. If the lines are double-spaced, then double the point size of each character

- 15. Write a program that calculates and prints the bill for a cellular telephone company. The company offers two types of service: regular and premium. Its rates vary, depending on the type of service. The rates are computed as follows:

**Regular service:** $10.00 plus first 50 minutes are free. Charges for over 50 minutes are $0.20 per minute.

**Premium service:** $25.00 plus:

  - a. For calls made from 6:00 a.m. to 6:00 p.m., the first 75 minutes are free; charges for more than 75 minutes are $0.10 per minute.

  - b. For calls made from 6:00 p.m. to 6:00 a.m., the first 100 minutes are free; charges for more than 100 minutes are $0.05 per minute.

Your program should prompt the user to enter an account number, a service code (type **char**), and the number of minutes the service was used. A service code of **r** or **R** means regular service; a service code of **p** or **P** means premium service. Treat any other character as an error. Your program should output the account number, type of service, number of minutes the telephone service was used, and the amount due from the user.

For the premium service, the customer may be using the service during the day and the night. Therefore, to calculate the bill, you must ask the user to input the number of minutes the service was used during the day and the number of minutes the service was used during the night.

- 16. Write a program to implement the algorithm that you designed in Exercise 22 of Chapter 1. (Assume that the account balance is stored in the file Ch4_Ex16_Data.txt.) Your program should output account balance before and after withdrawal and service charges. Also save the account balance after withdrawal in the file Ch4_Ex16_Output.txt.

- 17. You have several pictures of different sizes that you would like to frame. A local picture-framing store offers two types of frames—regular and fancy. The frames are available in white and can be ordered in any color the customer desires. Suppose that each frame is 1 inch wide. The cost of coloring the frame is $0.10 per inch. The cost of a regular frame is $0.15 per inch, and the cost of a fancy frame is $0.25 per inch. The cost of putting a cardboard paper behind the picture is $0.02 per square inch, and the cost of putting glass on top of the picture is $0.07 per square inch. The customer can also choose to put crowns on the corners, which costs $0.35 per crown. Write a program that prompts the user to input the following information and then output the cost of framing the picture:

  - a. The length and width, in inches, of the picture

  - b. The type of the frame

  - c. Customer's choice of color to color the frame

  - d. If the user wants to put the crowns, then the number of crowns

- 18. Samantha and Vikas are looking to buy a house in a new development. After looking at various models, the three models they like are colonial, split-entry, and single-story. The builder gave them the base price and the finished area in square feet of the three models. They want to know the model(s) with the least price per square foot. Write a program that accepts as input the base price and the finished area in square feet of the three models. The program outputs the model(s) with the least price per square foot.

- 19. One way to determine how healthy a person is is by measuring the body fat of the person. The formulas to determine the body fat for female and male are as follows:

  Body fat formula for women:

  A1 = (body weight × 0.732) + 8.987  
  A2 = wrist measurement (at fullest point) / 3.140  
  A3 = waist measurement (at navel) × 0.157  
  A4 = hip measurement (at fullest point) × 0.249  
  A5 = forearm measurement (at fullest point) × 0.434  
  B = A1 + A2 − A3 − A4 + A5  
  Body fat = body weight − B  
  Body fat percentage = body fat × 100 / body weight

  Body fat formula for men:

  A1 = (body weight × 1.082) + 94.42  
  A2 = wrist measurement × 4.15  
  B = A1 − A2  
  Body fat = body weight − B  
  Body fat percentage = body fat × 100 / body weight

  Write a program to calculate the body fat of a person.

![](img/f97f778697507bb6fdd80c5991210cba_288_0.png)

## CHAPTER 5

### Control Structures II (Repetition)

**IN THIS CHAPTER, YOU WILL:**

- Learn about repetition (looping) control structures
- Explore how to construct and use counter-controlled, sentinel-controlled, flag-controlled, and EOF-controlled repetition structures
- Examine `break` and `continue` statements
- Discover how to form and use nested control structures
- Learn how to avoid bugs by avoiding patches
- Learn how to debug loops

In Chapter 4, you saw how decisions are incorporated in programs. In this chapter, you learn how repetitions are incorporated in programs.

### Why Is Repetition Needed?

Suppose you want to add five numbers to find their average. From what you have learned so far, you could proceed as follows (assume that all variables are properly declared):

```
cin >> num1 >> num2 >> num3 >> num4 >> num5;  //read five numbers
sum = num1 + num2 + num3 + num4 + num5;       //add the numbers
average = sum / 5;                             //find the average
```

But suppose you want to add and average 100, 1000, or more numbers. You would have to declare that many variables and list them again in cin statements and, perhaps, again in the output statements. This takes an exorbitant amount of space and time. Also, if you want to run this program again with different values or with a different number of values, you have to rewrite the program.

Suppose you want to add the following numbers:

5 3 7 9 4

Consider the following statements, in which sum and num are variables of type int:

- `sum = 0;`
- `cin >> num;`
- `sum = sum + num;`

The first statement initializes sum to 0. Let us execute statements 2 and 3. Statement 2 stores 5 in num; statement 3 updates the value of sum by adding num to it. After statement 3, the value of sum is 5.

Let us repeat statements 2 and 3. After statement 2 (after the programming code reads the next number):

```
num = 3
```

After statement 3:

```
sum = sum + num = 5 + 3 = 8
```

At this point, sum contains the sum of the first two numbers. Let us again repeat statements 2 and 3 (a third time). After statement 2 (after the code reads the next number):

```
num = 7
```

After statement 3:

```
sum = sum + num = 8 + 7 = 15
```

Now, sum contains the sum of the first three numbers. If you repeat statements 2 and 3 two more times, sum will contain the sum of all five numbers.
