| CONTROL | DESCRIPTION |
|---|---|
| GridView | Displays multiple data items (such as rows in a database) in the form of rows, where each row has columns reflecting data fields. By manipulating the properties of this control, you can select, sort, and edit data items. |
| DataList | Displays multiple data items where you can supply templates for each item to display data fields in any way you choose. As with GridView, you can select, sort, and edit data items. |
| DetailsView | Displays a single data item in tabular form, with each row of the table relating to a data field. This control enables you to add, edit, and delete data items. |
| FormView | Displays a single data item using a template. As with DetailsView, this control enables you to add, edit, and delete data items. |
| ListView | Like DataList, but with support for pagination using DataPager and more template capabilities. |
| Repeater | Like DataList, but without selecting or editing capabilities. |
| DataPager | Allows pagination of ListView controls. |
| Chart | Displays data in a chart, such as a bar chart or pie chart. This control is examined in the next chapter. |

The dynamic data controls are covered in Chapter 42.

# Validation Web Server Controls

Validation controls provide a method of validating user input without (in most cases) your having to write any code at all. Whenever postback is initiated, each validation control checks the control it is validating and changes its IsValid property accordingly. If this property is false, then the user input for the validated control has failed validation. The page containing all the controls also has an IsValid property — if any of the validation controls has its version of this property set to false, then this will be false also. You can check this property from your server-side code and act on it.

Validation controls also have another function. Not only do they validate controls at runtime; they can also output helpful hints to users. Simply setting the ErrorMessage property to the text you want means users will see it when they attempt to postback invalid data.

The text stored in ErrorMessage may be output at the point where the validation control is located, or at a separate point, along with the messages from all other validation controls on a page. This latter behavior is achieved using the ValidationSummary control, which displays all error messages along with additional text as required.

On browsers that support it, these controls even generate client-side JavaScript functions to streamline their validation behavior. This means that in some cases postback won't even occur, because the validation controls can prevent this under certain circumstances and output error messages without involving the server.

All validation controls inherit from BaseValidator and thus share several important properties. Perhaps the most important is the ErrorMessage property discussed earlier in this section, with the ControlToValidate property coming in a close second. This property specifies the programmatic ID of the control that is being validated. Another important property is Display, which determines whether to place text at the validation summary position (if set to none), or at the validator position. You also have the choice to make space for the error message even when it is not being displayed (set Display to Static) or to dynamically allocate space when required, which might shift page contents around slightly (set Display to Dynamic). The following table describes the validation controls.