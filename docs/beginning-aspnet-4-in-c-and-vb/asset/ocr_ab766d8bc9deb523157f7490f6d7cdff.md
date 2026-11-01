The display shows several instances of the Person class that were constructed within the PersonList class. See Figure 39-8.

In some circumstances, it might be necessary to hide certain properties from the grid display — for this you can use the Browsable attribute as shown in the following code snippet. Any properties marked as non-browsable are not displayed in the property grid.

```
[Browsable(false)]
public bool IsEmployed
{
  .
}
```

The DataGridView uses this property to determine whether to display the property or hide it. In the absence of the attribute, the default is to display the property. If a property is read-only, the grid control will display the values from the object, but it will be read-only within the grid.

Any changes made in the grid view are reflected in the underlying objects — so, for example, if in the previous code the name of a person was changed within the user interface, the setter method for that property would be called.

![](bbox=[0.6, 0.1, 0.92, 0.42])

# DateTimePicker

The DateTimePicker allows users to select a date or time value (or both) in a number of different formats. You can display the DateTime-based value in any of the standard time and date formats. The Format property takes a DateTimePickerFormat enumeration that sets the format to Long, Short, Time, or Custom. If the Format property is set to DateTimePickerFormat.Custom, you can set the CustomFormat property to a string that represents the format.

There is both a Text property and a Value property. The Text property returns a text representation of the DateTime value, whereas the Value property returns the DateTime object. You can also set the maximum and minimum allowable date values with the MinDate and MaxDate properties.

When users click the down arrow, a calendar is displayed allowing the users to select a date in the calendar. Properties are available that allow you to change the appearance of the calendar by setting the title and month background colors as well as the foreground colors. The ShowUpDown property determines whether an UpDown arrow is displayed on the control. The currently highlighted value can be changed by clicking the up or down arrow.

# ErrorProvider

ErrorProvider is actually not a control but a component. When you drag a component to the Designer, it shows in the component tray under the Designer. The ErrorProvider flashes an icon next to a control when an error condition or validation failure exists. Suppose that you have a TextBox entry for an age and your business rules say that the age value cannot be greater than 63. If users try to enter an age greater than that, you must inform them that the age is greater than the allowable value and that they need to change the entered value. The check for a valid value takes place in the Validated event of the text box. If the validation fails, you call the SetError method, passing in the control that caused the error and a string that informs the user what the error is. An exclamation point icon starts flashing, indicating that an error has occurred, and when the user hovers over the icon the error text is displayed. Figure 39-9 shows the icon that is displayed when an invalid entry is made in the text box.

![](bbox=[0.7, 0.78, 0.92, 0.92])

If the validation of a field fails you would then call the SetIcon method of the ErrorProvider object and pass through the control that failed validation and an appropriate error message. The error is displayed as