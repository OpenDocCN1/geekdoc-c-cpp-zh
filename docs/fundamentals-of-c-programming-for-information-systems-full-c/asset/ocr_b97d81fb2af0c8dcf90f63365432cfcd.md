Similarly, make the necessary changes so that the user won’t be able to move away from the TextBox for unit price if the data entered into the TextBox is not a valid number. Display a message using a MessageBox. Highlight the data so that the user can type over it.

Make sure the user is able to close the form by clicking the Exit button, even when the data entered into a TextBox is not valid.

# Exercise 3-3

A retail clothing store offers a 10% discount if total sales is $50 or above and less than $100. If total sales is $100 or above, the store offers a 20% discount, and those who have a coupon get $10 off of total sales before applying the 20% discount.

Draw a flow chart that shows the logic for computing the subtotal (= total sales - all discounts).

Develop a new form named Exercise 3.3. You may develop the form within the existing project, Ch3_DecisionAndValidation, or a new project named Ch3_Exercises. Let the user enter the total sales into a TextBox on the form. Compute and display the total sales, coupon amount (if any), discount and subtotal, with the decimals aligned.

Hint: Use a Boolean variable for coupon. See Table 3-1 and Example 3 in this chapter. You may assign the value true or false to the Boolean variable within the program to test the code.

# Exercise 3-4

A hotel chain offers special discounts for customers who have a gold or platinum status:
Gold: 20% discount on reservations for 2 to 4 days and 30% discount for stays of 5 or more days
Platinum: 30% discount on reservations for 2 to 4 days and 40% discount for stays of 5 or more days.

Develop a new form named Exercise 3.4. You may develop the form within the existing project, Ch3_DecisionAndValidation, or a new project named Ch3_Exercises. Let the user enter the number of days, customer status (Gold or Platinum) and room rate/day into three different TextBoxes. Compute and display the total cost (= rate/day * number of days), discount and net amount (= total cost - discount), with the decimals aligned.