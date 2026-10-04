7. Next to the validator for the DateOfBirth box, drag a Comparator and set its properties as follows:

| Property | Value |
|---|---|n| Display | Dynamic |
| ErrorMessage | Please enter a valid date. |
| ControlToValidate | DateOfBirth |
| Operator | DataTypeCheck |
| Type | Date |

8. Set the TextMode of the Bio to Multiline and set its Height and Width properties to 75px and 300px, respectively.

9. Modify the table above to indicate that users can now do more than just change their password alone. Your Design View should look like Figure17-4.

![](bbox=[0.117, 0.423, 0.622, 0.683])

FIGURE 17-4

10. Double-click the Save button and in the Click event handler that VS added for you, write the following bolded code:

```
VB.NET
Protected Sub SaveButton_Click(sender As Object, e As EventArgs) Handles SaveButton.Click
If Page.IsValid Then
Profile.FirstName = FirstName.Text
Profile.LastName = LastName.Text
Profile.DateOfBirth = DateTime.Parse(DateOfBirth.Text)
Profile.Bio = Bio.Text
End If
End Sub
```