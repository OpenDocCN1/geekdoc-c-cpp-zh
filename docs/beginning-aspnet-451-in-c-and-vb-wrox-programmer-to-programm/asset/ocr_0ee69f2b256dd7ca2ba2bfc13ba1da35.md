# Understanding Profile | 639

| Text | AssociatedControlID |
|---|--|
| First name | FirstName |
| Last name | LastName |
| Date of birth | DateOfBirth |
| Biography | Bio |

+   5. In the second cell of the fifth row, draw a Button and set its ID to SaveButton and its Text to Save profile. Design View should look like Figure 17-3.

![](bbox=[0.156, 0.317, 0.788, 0.611])

FIGURE 17-3

+   6. In the last column of each of the first three rows, draw RequiredFieldValidator controls. Set their properties as follows, so validator lines up with a TextBox in the same row. Remember: you can set the Display property for all controls at by selecting the controls while pressing the Ctrl key first.

| ControlToValidate | Display | ErrorMessage |
|---|---|--|
| FirstName | Dynamic | First name is required. |
| LastName | Dynamic | Last name is required. |
| DateOfBirth | Dynamic | Date of birth is required. |