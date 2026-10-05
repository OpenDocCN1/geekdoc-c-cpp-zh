# Exercise 5-1 Enhance the Invoice Total application

In this exercise, you'll use if-else and switch statements to determine the discount percent for the Invoice Total application that's in figure 5-5.

Open the application and change the if-else statement

+   1. Open the application that's in the C:\C# 2010\Chapter05\InvoiceTotal directory.

+   2. Change the if-else statement to customers of type R with a subtotal that is greater or equal to $250 but less than $500 get a 25% discount and with a subtotal of $500 or more get a 30% discount. Next, change the if-else statement customers of type C always gets a 20% discount. Then, test the application to make sure this works.

+   3. Use code snippets to add another customer type to the if-else statement so customers of type T get a 40% discount for subtotals of less than $500, and a 50% discount for subtotals of $500 or more. Also, make sure that customer types aren't R, C, or T get a 10% discount. Then, test the application.

+   4. Test the application again, but use lowercase letters for the customer types. Note that these letters aren't evaluated as capital letters. Now, stop the debugging and modify the code so the users can enter either capital or lowercase letters for the customer types. Then, test the application to make sure it works correctly.

Use a switch statement with if-else statements to get the same results

+   5. Use a code snippet to enter the start of a switch statement right after the if-else statement. Next, enhance this code so the switch statement provides the structure for handling the three cases for customer types: R, C, and T (but not r, and t). Then, within each of these cases, you can copy the related code from the if-else statement above to provide for the discounts that are based on subtotal variations. In other words, the if-else statements will be nested within the switch cases.

+   7. When you're finished, close the application.