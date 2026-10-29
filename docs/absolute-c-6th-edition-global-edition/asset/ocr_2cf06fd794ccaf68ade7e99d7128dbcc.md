2. In order to manage their funds efficiently, a person deposits an amount of money in a bank account. They withdraw a fixed portion on the fifth day of every month. The bank credits the interest accumulated on their balance on the last day of every month. Write a program that inputs the initial deposit made, the interest rate provided by bank, and the fixed amount withdrawn every month. Calculate the number of months the amount (including the credited interest) can be utilized. (Hint: Use a loop)

Note: Check for boundary conditions – If the interest earned every month is greater than the fixed withdrawal amount, the program should print that message and return.

3. An organization intends to get people to sponsor the education of underprivileged children. As part of their program, they launch a website where people can register by entering their details and the amount (in USD) they wish to sponsor each month. The website calculates the number of children the donor can sponsor based on the amount required to educate one child.

Write a program that inputs the amount required for one child’s education, and the amount a person is willing to sponsor, and calculates how many children can be sponsored by that person. The program should also print how much of the person’s amount is remaining after calculating the number of children, and suggest how many more dollars would educate another child. (Hint: Use a do while loop)

4. Write a program that finds and prints all of the prime numbers between 3 and 100. A prime number is a number that can only be divided by one and itself (i.e., 3, 5, 7, 11, 13, 17, ...).

One way to solve this problem is to use a doubly-nested loop. The outer loop can iterate from 3 to 100, while the inner loop checks to see whether the counter value for the outer loop is prime. One way to decide whether the number n is prime is to loop from 2 to n – 1; if any of these numbers evenly divides n, then n cannot be prime. If none of the values from 2 to n – 1 evenly divide n, then n must be prime. (Note that there are several easy ways to make this algorithm more efficient.)

5. In cryptarithmetic puzzles, mathematical equations are written using letters. Each letter can be a digit from 0 to 9, but no two letters can be the same. Here is a sample problem:

SEND + MORE = MONEY
A solution to the puzzle is S = 9, R = 8, O = 0, M = 1, Y = 2, E = 5, N = 6, D = 7.
Write a program that finds solutions to the following cryptarithmetic puzzle:

TOO + TOO + TOO + TOO = GOOD
The simplest technique is to use a nested loop for each unique letter (in this case T, O, G, D). The loops would systematically assign the digits from 0–9 to each letter. For example, it might first try T = 0, O = 0, G = 0, D = 0, then T = 0, O = 0, G = 0, D = 1, then T = 0, O = 0, G = 0, D = 2, etc. up to T = 9, O = 9, G = 9, D = 9.

![](bbox=[0.07, 0.72, 0.16, 0.85])