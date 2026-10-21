# Chapter 21

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