
- 8. Write a program that mimics a calculator. The program should take as input two integers and the operation to be performed. It should then output the numbers, the operator, and the result. (For division, if the denominator is zero, output an appropriate message.) Some sample outputs follow:

  ```
  3 + 4 = 7
  13 * 5 = 65
  ```

- 9. Redo Exercise 8 to handle floating-point numbers. (Format your output to two decimal places.)

- 10. Redo Programming Exercise 16 of Chapter 2, taking into account that your parents buy additional savings bonds for you as follows:

  - a. If you do not spend any money to buy savings bonds, then because you had a summer job, your parents buy savings bonds for you in an amount equal to 1% of the money you save after paying taxes and buying clothes, other accessories, and school supplies.

  - b. If you spend up to 25% of your net income to buy savings bonds, your parents spend $0.25 for each dollar you spend to buy savings bonds, plus money equal to 1% of the money you save after paying taxes and buying clothes, other accessories, and school supplies.

  - c. If you spend more than 25% of your net income to buy savings bonds, your parents spend $0.40 for each dollar you spend to buy savings bonds, plus money equal to 2% of the money you save after paying taxes and buying clothes, other accessories, and school supplies.

- 11. Write a program that implements the algorithm given in Example 1-3 (Chapter 1), which determines the monthly wages of a salesperson.

- 12. Write a program that implements the algorithm that you designed in Exercise 34 of this chapter.

- 13. The number of lines that can be printed on a paper depends on the paper size, the point size of each character in a line, whether lines are double-spaced or single-spaced, the top and bottom margin, and the left and right margins of the paper. Assume that all characters are of the same point size, and all lines are either single-spaced or double-spaced. Note that 1 inch = 72 points. Moreover, assume that the lines are printed along the width of the paper. For example, if the length of the paper is 11 inches and width is 8.5 inches, then the maximum length of a line is 8.5 inches. Write a program that calculates the number of characters in a line and the number of lines that can be printed on a paper based on the following input from the user:

  - a. The length and width, in inches, of the paper
  - b. The top, bottom, left, and right margins
  - c. The point size of a line
  - d. If the lines are double-spaced, then double the point size of each character

- 14. Write a program that calculates and prints the bill for a cellular telephone company. The company offers two types of service: regular and premium. Its rates vary, depending on the type of service. The rates are computed as follows:

  Regular service: $10.00 plus first 50 minutes are free. Charges for over 50 minutes are $0.20 per minute.

  Premium service: $25.00 plus:

  - a. For calls made from 6:00 a.m. to 6:00 p.m., the first 75 minutes are free; charges for more than 75 minutes are $0.10 per minute.

  - b. For calls made from 6:00 p.m. to 6:00 a.m., the first 100 minutes are free; charges for more than 100 minutes are $0.05 per minute.

  Your program should prompt the user to enter an account number, a service code (type char), and the number of minutes the service was used. A service code of r or R means regular service; a service code of p or P means premium service. Treat any other character as an error. Your program should output the account number, type of service, number of minutes the telephone service was used, and the amount due from the user.

  For the premium service, the customer may be using the service during the day and the night. Therefore, to calculate the bill, you must ask the user to input the number of minutes the service was used during the day and the number of minutes the service was used during the night.

- 15. Write a program to implement the algorithm that you designed in Exercise 22 of Chapter 1. (Assume that the account balance is stored in the file Ch4_Ex15_Data.txt.) Your program should output account balance before and after withdrawal and service charges. Also save the account balance after withdrawal in the file Ch4_Ex15_Output.txt.

- 16. A new author is in the process of negotiating a contract for a new romance novel. The publisher is offering three options. In the first option, the author is paid $5,000 upon delivery of the final manuscript and $20,000 when the novel is published. In the second option, the author is paid 12.5% of the net price of the novel for each copy of the novel sold. In the third option, the author is paid 10% of the net price for the first 4000 copies sold, and 14% of the net price for the copies sold over 4000. The author has some idea about the number of copies that will be sold and would like to have an estimate of the royalties generated under each option. Write a program that prompts the author to enter the net price of each copy of the novel and the estimated number of copies that will be sold. The program then outputs the royalties under each option and the best option the author could choose. (Use appropriate named constants to store the special values such as royalties rates and fixed royalties.)

- 17. Samantha and Vikas are looking to buy a house in a new development. After looking at various models, the three models they like are colonial, split-entry, and single-story. The builder gave them the base price and the finished area in square feet of the three models. They want to know the model(s) with the least price per square foot. Write a program that accepts as input the base price and the finished area in square feet of the three models. The program outputs the model(s) with the least price per square foot.

- 18. One way to determine how healthy a person is by measuring the body fat of the person. The formulas to determine the body fat for female and male are as follows:

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

- 19. Ron bought several acres of farm to grow and sell vegetables. Suppose that Ron wants to grow a maximum of two types of vegetables. Write a program that prompts Ron or the user to do the following:

  - 1. Enter the total farm area in acres.
  - 2. The number of vegetables (one or two) that the user wants to grow.
  - 3. If the user wants to grow two types of vegetables, then specify the portion, as a percentage, of the farm land used for each type of vegetable.
  - 4. Enter the seed cost, plantation cost, fertilizing cost, labor cost, for each acre.
  - 5. Enter vegetable selling price per acre.
  - 6. Output the total revenue.
  - 7. Output the profit/loss.

- 20. The cost of renting a room at a hotel is, say $100.00 per night. For special occasions, such as a wedding or a conference, the hotel offers a special discount as follows: If the number of rooms booked is at least 10, the discount is 10%; at least 20, the discount is 20%; and at least 30, the discount is 30%. Also if rooms are booked for at least 3 days, then there is an additional 5% discount. Write a program that prompts the user to enter the cost of renting one room, the number of rooms booked, the number of days the rooms are booked, and the sales tax (as a percent). The program outputs the cost of renting one room, the discount on each room as a percent, the number of rooms booked, the number of days the rooms are booked, the total cost of the rooms, the sales tax, and the total billing amount. Your program must use appropriate named constants to store special values such as various discounts.

- 21. Let l be a line in the x-y plane. If l is a vertical line, its equation is x = a for some real number a. Suppose l is not a vertical line and its slope is m. Then the equation of l is y = mx + b, where b is the y-intercept. If l passes through the point (x₀, y₀), then the equation of l can be written as y − y₀ = m(x − x₀). If (x₁, y₁) and (x₂, y₂) are two points in the x-y plane and x₁ ≠ x₂, the slope of the line passing through those points is m = (y₂ − y₁) / (x₂ − x₁). Write a program that prompts the user to enter two points in the x-y plane. The program outputs the equation of the line and uses if statements to determine and output whether the line is vertical, horizontal, increasing, or decreasing. If l is a nonvertical line, output its equation in the form y = mx + b.

- 22. The first 11 prime integers are 2, 3, 5, 7, 11, 13, 17, 19, 23, 29, and 31. A positive integer between 1 and 1000 (inclusive), other than the first 11 prime integers, is prime if it is not divisible by 2, 3, 5, 7, 11, 13, 17, 19, 23, 29, and 31. Write a program that prompts the user to enter a positive integer between 1 and 1000 (inclusive) and that outputs whether the number is prime. If the number is not prime, then output all the numbers, from the list of the first 11 prime integers, which divide the number.

![](img/d0be7fc6d804b63484835c6c8bc67a07_311_0.png)
