you can set the Display property for all controls at once by selecting the controls while pressing the Ctrl key.

| CONTROLTOVALIDATE | DISPLAY | ERRORMESSAGE |
|---|---|---|
| FirstName | Dynamic | First name is required. |
| LastName | Dynamic | Last name is required. |
| DateOfBirth | Dynamic | Date of birth is required. |

7. Next to the validator for the DateOfBirth box, drag a CompareValidator and set its properties as follows:

| PROPERTY | VALUE |
|---|---|
| Display | Dynamic |
| ErrorMessage | Please enter a valid date. |
| ControlToValidate | DateOfBirth |
| Operator | DataTypeCheck |
| Type | Date |

8. Set the TextMode of the Bio control to MultiLine and set its Height and Width properties to 75px and 300px, respectively.

9. Modify the text above the table to indicate that users can now do more than just change their password alone. Your Design View should look like Figure 17-4.

![](bbox=[0.13, 0.78, 0.82, 0.89])

FIGURE 17-4