# Table 3-1: Relational operators

| Relational operator | What it means | Examples |
|---|---|---|
| > | Greater than | if (roomCapacity > enrollment) |
| < | Less than | if (dateDue < DateTime.Today) |
| >= | Greater than or equal to | if (examScore >= 90) |
| <= | Less than or equal to | if (dateOfBirth <= DateTime.Parse("12/31/1980")) |
| == (combination of two "=" signs) | Equal to | if (city == "Oshkosh") // city is string type
if (inState == true) // inState is bool type
// The expression if (inState == true) may be replaced by
// if (inState), because inState itself is true or false. |
| != | Not equal to | if (middleInitial != 'C') // middleInitial is of char type. |

# Tutorial 1: Ice Cream Total with Discount

This tutorial develops the updated version of Tutorial 3 from Chapter 1 to include a discount, as represented in the flowchart in Figure 3-2.

Step 1-1: Open the project, Ch3_DecisionAndValidation from the Tutorial_Starts folder. Open the form IceCreamTotalDiscounted.
Edit Program.cs file to specify IceCreamTotalDiscounted as the form to be run.

Step 1-2: Modify the code for computing total cost, as shown in Figure 3-3: The changes include
Lines 40-43: Add if else statement to compute discountPercent.
Lines 46-52: Uncomment statements to compute discount, net cost and total cost.
Lines 57-60: Uncomment statements to display subtotal, discount and net cost.
Lines 62-63: Add statements to display sales tax and net cost.

Test the program with combinations of unit price and number of scoops that yield subtotals that are less than 10, equal to 10 and more than 10.