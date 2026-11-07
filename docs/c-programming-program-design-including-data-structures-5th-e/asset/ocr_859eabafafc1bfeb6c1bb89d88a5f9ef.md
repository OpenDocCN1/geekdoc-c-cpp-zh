+   • `.` (period), `?` (question mark), `;` (semicolon), and `:` (colon). (Your program may store the output in a file.)

+   4. Write a program that prompts the user to input a string. The program then uses the function `substr` to remove all the vowels from the string. For example, if `str = "There"`, then after removing all the vowels, `str = "Thr"`. After removing all the vowels, output the string. Your program must contain a function to remove all the vowels and a function to determine whether a character is a vowel.

+   5. Write a program that can be used to calculate the federal tax. The tax is calculated as follows: For single people, the standard exemption is $4,000; for married people, the standard exemption is $7,000. A person can also put up to 6% of his or her gross income in a pension plan. The tax rates are as follows: If the taxable income is:

+   - Between $0 and $15,000, the tax rate is 15%.
+   - Between $15,001 and $40,000, the tax is $2,250 plus 25% of the taxable income over $15,000.
+   - Over $40,000, the tax is $8,460 plus 35% of the taxable income over $40,000.

Prompt the user to enter the following information:

+   - Marital status
+   - If the marital status is “married,” ask for the number of children under the age of 14
+   - Gross salary (If the marital status is “married” and both spouses have income, enter the combined salary.)
+   - Percentage of gross income contributed to a pension fund

Your program must consist of at least the following functions:

+   a. Function `getData`: This function asks the user to enter the relevant data.
+   b. Function `taxAmount`: This function computes and returns the tax owed.

To calculate the taxable income, subtract the sum of the standard exemption, the amount contributed to a pension plan, and the personal exemption, which is $1,500 per person. (Note that if a married couple has two children under the age of 14, then the personal exemption is $1,500 * 4 = $6,000.)

+   6. A set of integers *a*, *b*, and *c* is called a Pythagorean triple if *a*² + *b*² = *c*². For example, the integers 3, 4, and 5 form a Pythagorean triple because 3² + 4² = 5². To find Pythagorean triples, use the following formula. Let *m* and *n* be integers. If *a* = *m*² − *n*², *b* = 2*mn*, and *c* = *m*² + *n*², then *a*, *b*, and *c* are a Pythagorean triple. Write a program that prompts the user to enter values for *m* and *n* and then outputs the Pythagorean triple corresponding to *m* and *n*.

+   7. **(Fraction calculator)** Write a program that lets the user perform arithmetic operations on fractions. Fractions are of the form *a/b*, in which *a* and *b* are integers and *b* ≠ 0. Your program must be menu driven, allowing the user to