
property for the upperValuesLimit control to 49; this is the value displayed initially in the control. If you also set the ReadOnly property value for each of the NumericUpDown controls to True, this prevents the entry of a value from the keyboard. You are using the NumericUpDown control very simply here. You can change the up down increment by setting the Increment property value. The Increment property is of type Decimal so you can set this to non-integral values, too.

![](img/2359b0c604600c58fba3539c738a356e_1110_0.png)

Figure 21-25

You can set the values of the (Name) property for the ComboBox controls in the lower group box to lowerStarsLimits and upperStarsLimits. You can enter values to be displayed in a ComboBox quite easily. Click the small arrow at the top right of the leftmost ComboBox control to display the menu shown in Figure 21-26.

![](img/2359b0c604600c58fba3539c738a356e_1110_1.png)

Figure 21-26

## Chapter 21

Select the Edit Items menu item at the bottom of the menu to display the dialog window for the String Collection Editor shown in Figure 21-27.

![](img/2359b0c604600c58fba3539c738a356e_1111_0.png)

Figure 21-27 shows the values entered for the ComboBox control on the left. For the ComboBox control on the right you can enter the values from 2 to 9 inclusive.

The ComboBox is not ideal for this application because it allows text input as well as selection from a list; you want to have a limit value selected only from the list. The control gets its name, ComboBox, because it combines the function of a ListBox control that allows selection from a list with that of a TextBox control that provides for text input.

### Getting the Data from the Dialog Controls

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

```
InitializeComponent();
//
//TODO: Add the constructor code here
//
}
```

You’ll also need some public properties defined in the dialog class to make the limits accessible from the application window object:

```
public:
    property int LowerValuesLimit
    {
        int get() { return lowerValuesLimit; }

        void set(int limit)
        {
            lowerValuesLimit = limit;
            lowerValuesLimits->Value = limit;        // Set as selected in NumericUpDown
        }
    }
    property int UpperValuesLimit
    {
        int get() { return upperValuesLimit; }

        void set(int limit)
        {
            upperValuesLimit = limit;
            upperValuesLimits->Value = limit;        // Set as selected in NumericUpDown
        }
    }
    property int LowerStarsLimit
    {
        int get() { return lowerStarsLimit; }

        void set(int limit)
        {
            lowerStarsLimit = limit;
            lowerStarsLimits->SelectedItem = limit;  // Set as selected in ComboBox
            lowerStarsLimits->SelectedIndex =        // Set index for selected item
                lowerStarsLimits->FindString(limit.ToString());
        }
    }

    property int UpperStarsLimit
    {
        int get() { return upperStarsLimit; }

        void set(int limit)
        {
            upperStarsLimit = limit;
            upperStarsLimits->SelectedItem = limit;  // Set as selected in ComboBox
            upperStarsLimits->SelectedIndex =        // Set index for selected item
                upperStarsLimits->FindString(limit.ToString());
        }
    }
```

## Chapter 21

The get() function for each property returns the value of the corresponding private member of the dialog class. The set() function sets the value of the data member and also updates the control in the dialog box so that the value set becomes the selected value. The SelectedIndex property value is the index to the selected item. You set this using the FindString() function for the ComboBox control that returns the index value for the first occurrence of the argument in the control’s collection of items. The value at this position is displayed initially in the control.

Add a Click event handler for the OK button in the EuroLimitsDialog class by double-clicking the button in the Design window. You won’t need to implement a handler for the Cancel button. You can implement the OK button handler like this:

```
System::Void euroOK_Click(System::Object^ sender, System::EventArgs^ e)
{
    ::DialogResult result;

    // get the limits for values
    int valuesLower = Decimal::ToInt32(lowerValuesLimits->Value);
    int valuesUpper = Decimal::ToInt32(upperValuesLimits->Value);
    if(valuesUpper - valuesLower < 4)            // Check for an adequate range
    {
        result = MessageBox::Show(this,            // Range insufficient so
            "Upper values limit: "+valuesUpper +   // display message box
            " Lower values limit: "+ valuesLower+
            "\nUpper values limit must be at least 4 greater that the lower limit."+
            "\nTry Again.",
            "Limits Invalid",
            MessageBoxButtons::OKCancel,
            MessageBoxIcon::Error);

        if(result == ::DialogResult::OK)            // If message box OK clicked
            DialogResult = ::DialogResult::None;    // prevent dialog from closing
        else                                        // Messag box Cancel clicked
            DialogResult = ::DialogResult::Cancel;  // so close the dialog
        return;
    }

    // Get stars limits
    int starsLower = lowerStarsLimits->SelectedItem == nullptr ?
                        lowerStarsLimit :
                        Int32::Parse(lowerStarsLimits->SelectedItem->ToString());

    int starsUpper = upperStarsLimits->SelectedItem == nullptr ?
                        upperStarsLimit :
                        Int32::Parse(upperStarsLimits->SelectedItem->ToString());

    if(starsUpper - starsLower < 1)            // Check for an adequate range
    {
        result = MessageBox::Show(this,            // Range insufficient so
            "Upper stars limit: "+starsUpper +     // so display message box
            " Lower stars limit: "+ starsLower+
            "\nUpper stars limit must be at least 1 greater that the lower limit."+
            "\nTry Again.",
            "Limits Invalid",
```

```
MessageBoxButtons::OKCancel,
MessageBoxIcon::Error);
if(result == ::DialogResult::OK)                // If message box OK clicked
    DialogResult = ::DialogResult::None;          // prevent dialog from closing
else                                           // Message box Cancel clicked
    DialogResult = ::DialogResult::Cancel;       // so close the dialog
}
// Store the new limits
lowerValuesLimit = valuesLower;
upperValuesLimit = valuesUpper;
lowerStarsLimit = starsLower;
upperStarsLimit = starsUpper;
}
```

The Value property for a NumericUpDown control returns a value of type Decimal. To convert this to type Int32 you pass it as the argument to the static ToInt32() function in the Decimal class. The value that this function returns is automatically unboxed so that it can be stored in the variable of type int.

The value returned by the SelectedItem property for a ComboBox control is of type Object^, so to be on the safe side you check whether it is null. If it is null, you set the local variable to the current value recorded in the dialog object; if it isn’t null, you store the value represented by the SelectedItem property. You can’t store the value directly, but calling the ToString() function for the object produces a string representation of the object that you are then able to convert to type int using the static Parse() function in the Int32 class.

You will need a private member of the Form1 class that stores a handle to the new dialog box:

```
private:
    EuroLimitsDialog^ euroLimitsDialog;    // Dialog to set Euromillions limits
```

You can add the following statements to the end of the code in the Form1 class constructor to create the dialog object and update the properties for the stars limit values:

```
euroLimitsDialog = gcnew EuroLimitsDialog;
euroLimitsDialog->LowerStarsLimit = euroStarsLowerLimit;
euroLimitsDialog->UpperStarsLimit = euroStarsUpperLimit;
```

By setting the LowerStarsLimit and UpperStarsLimit properties for the dialog object, you ensure that the ComboBox controls show these values when the dialog box is initially displayed. If there is no selected item set for a ComboBox control, it displays nothing initially.

Don’t forget to add the #include directive for the EuroLimitsDialog class definition to Form1.h:

```
#include "EuroLimitsDialog.h"
```

### Disabling Input Controls

When the Limits > Upper menu item is clicked, you want to prevent the input for a lower limit being entered, and when the Limits > Lower menu item is selected, you want to prevent input for an upper limit value. You can add a couple of member functions to the EuroLimitsDialog class to make this possible:
