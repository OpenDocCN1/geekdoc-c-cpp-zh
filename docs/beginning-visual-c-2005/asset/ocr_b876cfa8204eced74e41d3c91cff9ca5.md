# Chapter 21

Select the Edit Items menu item at the bottom of the menu to display the dialog window for the String Collection Editor shown in Figure 21-27.

![](bbox=[0.27, 0.14, 0.67, 0.44])

Figure 21-27 shows the values entered for the ComboBox control on the left. For the ComboBox control on the right you can enter the values from 2 to 9 inclusive.

The ComboBox is not ideal for this application because it allows text input as well as selection from a list; you want to have a limit value selected only from the list. The control gets its name, ComboBox, because it combines the function of a ListBox control that allows selection from a list with that of a TextBox control that provides for text input.

# Getting the Data from the Dialog Controls

You’ll get the limit values back from the controls in essentially the same way as you did for the dialog box for Lotto limits. You can add some new data members to the EuroLimitsDialog class to hold the user limit values first:

```
private:
    int lowerValuesLimit;
    int upperValuesLimit;
    int lowerStarsLimit;
    int upperStarsLimit;
```

To be on the safe side you had better initialize these members in the class constructor:

```
EuroLimitsDialog(void)
    :lowerValuesLimit(1)
    ,upperValuesLimit(50)
    ,lowerStarsLimit(1)
    ,upperStarsLimit(9)
{
```