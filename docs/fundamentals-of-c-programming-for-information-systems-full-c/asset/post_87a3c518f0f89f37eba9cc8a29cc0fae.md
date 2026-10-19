
## Mixing Different Data Types in a Boolean Expression

The rules you learned in Chapter 2 about mixing different data types in a formula (mathematical expression) involving numbers also apply to Boolean expressions—that is, you may mix different real and integer data types in a Boolean expression, but you cannot mix a decimal with a float or double without explicit conversion. For example, the expression in the following if statement is invalid:

```
decimal price = 12.5m;
if (price > 10.5) // invalid; cannot compare a decimal to double
```

The expression should be changed to

```
if (price > 10.5m)      // valid
```

The following comparisons are valid:

```
decimal price = 12.5m;
if (price > 10)   // valid; decimal and integer types may be mixed
```

```
float price = 12.5f;
if (price > 10.5) // valid; float and double types may be mixed
```

An if statement may use one or more of the following relational operators to compare data items in a Boolean expression:

## if Statement with No else Clause

Example 2: An alternate way to represent the decision structure shown in Figure 3-2 is to remove the statements in the false path and place them before the decision structure, as shown below:

![](img/143bad48262566137acc9c41f668a88f_105_0.png)

The following program shows the modified if statement to implement the new decision structure:

```
bool freeTopping;
if ((subTotal >= 10) || (scoops >=3))
{
    discountPercent = 20;        // processed if either (subTotal >= 10) or (scoops >=3),
    freeTopping = true;          // that is, if one of the two Boolean expressions is true.
}
else
{
    discountPercent = 0;   // processed if both Boolean expressions are not true
    freeTopping = false; // that is, if both are false.
}
```

Step 1-6: Modify the if statement to include the revised criteria. Run and test the form with different combinations of subtotal and scoops so that (1) both Boolean expressions are false, (2) only the first expression is true, (3) only the second expression is true and (4) both expressions are true. Observe the result in each case.

Change the logical operator from "||" (Or) to "&&" (And), run the form and observe the difference under the four different combinations of subtotal and scoops. Change the logical operator back to "||"

The expression ((subTotal >= 10) || (scoops >=3)) checks whether subtotal is at least 10 or scoops is at least 3. An alternative to do the same thing is to check whether the expression ((subTotal < 10) and (scoops < 3)) is false—that is, both subtotal and scoops are not below the required limit. Note that the expressions have the "<" operator in place of ">=". Further, "Or" is replaced by "And."

You can use the "!" (Not) operator to check whether the expression is false, as follows:

```
if (!((subTotal < 10) && (scoops < 3)))
```

Step 1-7: Change the if statement to: if (!((subTotal < 10) && (scoops<3))). Run the form and observe the difference under the four different combinations of subtotal and scoops specified in Step 1-6. Observe the result in each case. Now, change "&&" to "||" as follows:

```
bool freeTopping;
if (!((subTotal < 10) || (scoops < 3)))
{
    discountPercent = 20;
    freeTopping = true;
}
else
{
    discountPercent = 0;
    freeTopping = false;
}
```

This won’t give the desired result. If any one of the two Boolean expressions is false, then the combined expression, ((subTotal < 10) || (scoops < 3)) is true, which makes (!((subTotal < 10) || (scoops < 3))) false, resulting in no discount.

Run the form and observe the difference under the four different combinations of subtotal and scoops. Observe the result in each case.

## Review Questions

What would be the output displayed in the ListBox lstOutput by the following programs?

```
3.1
int totalAmt = 80, percentDiscount = 5;
if (totalAmt >= 100)
    percentDiscount = 20;
lstOutput.Items.Add(percentDiscount);
```

```
3.2
int totalAmt = 80;
int percentDiscount = 5;
if (totalAmt >= 100)
    percentDiscount = 20;
else
    percentDiscount = 0;
lstOutput.Items.Add(percentDiscount);
```

```
3.3
int ACT = 23;
float GPA = 3.2F;
if ((ACT >= 24) || (GPA >= 3))
    lstOutput.Items.Add("Admit");
else
    lstOutput.Items.Add("Deny");
```

```
3.4
int ACT = 23;
float GPA = 3.2F;
if ((ACT >= 24) && (GPA >= 3))
    lstOutput.Items.Add("Admit");
else
    lstOutput.Items.Add("Deny");
```

```
3.5
int ACT = 23;
float GPA = 3.2F;
if (!((ACT >= 24) || (GPA >= 3)))
    lstOutput.Items.Add("Admit");
else
    lstOutput.Items.Add("Deny");
```

```
3.6
int ACT = 23;
float GPA = 3.2F;
if (!((ACT >= 24) && (GPA >= 3)))
    lstOutput.Items.Add("Admit");
else
    lstOutput.Items.Add("Deny");
```

## 3.3 if else if Statement

Consider a grading scale with a minimum of 90, 80 and 70 for A, B and C, respectively (anything below 70 is an F). The flowchart that represents the decision structure would look as follows:

![](img/143bad48262566137acc9c41f668a88f_111_0.png)

Example 4: The following program uses the if else if structure to compute the letter grade based on the decision structure represented by the flowchart. In addition to the grade, the program also computes the grade point.

```
string letterGrade;
int gradePoints;
if (totalScore >= 90)
{
    letterGrade = "A";
    gradePoints = 4;
}
else if (totalScore >= 80)
{
    letterGrade = "B";
    gradePoints = 3;
}
else if (totalScore >= 70)
{
    letterGrade = "C";
    gradePoints = 2;
}
else
{
    letterGrade = "F";
    gradePoints =0;
}
```

Step 2-2: Review the user interface controls specified in Table 3-3.

### Table 3-3: Controls on ComputeGrade form

| Purpose | Type of control | Property | Setting |
|---|---|---|---|
| Enter total score | TextBox | Name | txtScore |
| Enter attendance % | TextBox | Name | txtAttendance |
| Display grade | Label | Name | txtGrade |
| Display label for total score | Label | Text | Score: |
| Display label for attendance | Label | Text | Attendance: |
| Display label for grade | Label | Text | Grade: |
| Compute grade | Button | Name | btnGrade |
| Compute grade | Button | Text | Compute Grade |

First, you develop the code to compute grade based on just the total points, ignoring attendance.

Step 2-3: Add the following code to the click event handler of btnGrade to compute grade based only on score.

### Figure 3-5: Code to compute grade based only on score.

```
20  private void btnGrade_Click(object sender, EventArgs e)
21  {
22      string letterGrade;
23      float totalScore = float.Parse(txtScore.Text);
24
25      // Compute grade using if else if, based only on score:
26
27      if (totalScore >= 90)
28          letterGrade = "A";
29      else if (totalScore >= 80)
30          letterGrade = "B";
31      else if (totalScore >= 70)
32          letterGrade = "C";
33      else
34          letterGrade = "F";
35
36      // Display grade:
37      lblGrade.Text = letterGrade;
```

Step 2-4: Change the startup form to ComputeGrade, and run the project with values of score in the range 0 to 100, a value above 100 and one negative value. No data for attendance is needed for this version of the program.

## 3.5 The switch Statement

The switch statement provides a convenient way to branch to one of many paths based on the value of a variable or an expression. How does it differ from an if statement with else if clause? Let’s look at the code to determine the discount percent for a hotel reservation based on the discount type (“AAA,” “Best Rate,” “Government” or “Senior”) for a hotel guest.

Here is the if statement with else if clause to determine the discount:

```
float discountPercent;
if (discountType == "AAA")
    discountPercent = 10;
else if (discountType == "Best Rate")
    discountPercent = 5;
else if (discountType == "Government")
    discountPercent = 15;
else if (discountType == "Senior")
    discountPercent = 12.5F;
else
    discountPercent = 0;
```

The corresponding switch statement is

```
float discountPercent;
switch (discountType)
{
    case "AAA":
        discountPercent = 10;
        break;
    case "Best Rate":
        discountPercent = 5;
        break;
    case "Senior":
        discountPercent = 12.5F;
        break;
    case "Government":
        discountPercent = 15;
        break;
    default:
        discountPercent = 0;
        break;
}
```

The switch statement checks the value of the test variable, discountType, and branches to one of the first four paths based on its value (“AAA,” “Best Rate,” “Government” or “Senior”). If the value does not match any one of the four values, the statement under default is processed.

Note that there is a break statement in each path, which causes the program to skip the rest of the switch statement. For example, if the discountType is “Best Rate,” then the program assigns the value 5 to discountRate, and the break statement causes it to skip checking for the values “Government” and “Senior” that are specified in the rest of the case statements.
