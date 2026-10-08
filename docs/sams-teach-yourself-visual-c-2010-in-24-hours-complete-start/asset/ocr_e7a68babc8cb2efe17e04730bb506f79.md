# # Try It Yourself

# ## Validating Input

To add validation rules to the AddressBook application, follow these steps.

+   1. Add the validation rule shown in Listing 18.16 to the AddressBook application.

+   2. Add a new validation rule to the AddressBook application named *EmptyStringValidationRule* that validates that the object to validate is not an empty string.

+   3. Add the ControlTemplate shown in Listing 18.17 to the Window.Resources element of the ContactEditor.xaml file.

+   4. Modify the ContactEditor.xaml file so that the bindings for the following elements set the *Validation.ErrorTemplate* property and include the indicated validation rule:

| Element | Validation Rule |
| :--- | :--- |
| First Name | *EmptyStringValidationRule* |
| Last Name | *EmptyStringValidationRule* |
| Home Phone | *PhoneNumberValidationRule* |
| Mobile Phone | *PhoneNumberValidationRule* |
| Work Phone | *PhoneNumberValidationRule* |
| Pager | *PhoneNumberValidationRule* |
| Fax | *PhoneNumberValidationRule* |

+   5. Run the application and press the Add Contact toolbar button to display the ContactEditor form. Enter some invalid data and observe that the visual representation of the fields that are invalid changes to the one defined by the ControlTemplate.

# # Summary

In this hour, you learned about data binding in WPF and added bindings to the PhotoViewer application to make it more complete. From there, you learned how data converters can change the value from one side of the binding to something the other side of the binding will accept. You then learned about binding to collections and