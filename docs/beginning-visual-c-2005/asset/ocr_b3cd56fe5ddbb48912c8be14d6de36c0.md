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

# Disabling Input Controls

When the Limits > Upper menu item is clicked, you want to prevent the input for a lower limit being entered, and when the Limits > Lower menu item is selected, you want to prevent input for an upper limit value. You can add a couple of member functions to the EuroLimitsDialog class to make this possible: