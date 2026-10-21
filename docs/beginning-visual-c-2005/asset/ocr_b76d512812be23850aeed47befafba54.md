right-clicked is already stored in the contextButton member because the buttonContextMenu_Opening() handler that you added earlier is executed first.

```
System::Void chooseValue_Click(System::Object^ sender, System::EventArgs^ e)
{
    array<int>^ values;                    // Array to store current button values
    array<Button^>^ theButtons;            // Handle to aray of buttons

    // Check if the button is in the lottoValues group box
    if(lottoValues->Controls->Contains(contextButton))
    {
        // the button is from the lotto group...
        array<Button^>^ buttons = {lottoValue1, lottoValue2, lottoValue3,
                                   lottoValue4, lottoValue5, lottoValue6};
        theButtons = buttons;               // Store array handle at outer scope
        values = GetButtonValues(buttons);  // Get array of button values

        // Set up the dialog ready to be shown
        userValueDialog->Values = values = GetButtonValues(buttons);
        userValueDialog->LowerLimit = lottoUserMinimum;
        userValueDialog->UpperLimit = lottoUserMaximum;
        userValueDialog->SetLabelText(lottoUserMinimum, lottoUserMaximum);
    }
    // Check if the button is in the euroValues group box
    else if(euroValues->Controls->Contains(contextButton))
    {
        // The button is in the Values group...
        array<Button^>^ buttons = {euroValue1, euroValue2, euroValue3,
                                   euroValue4, euroValue5};
        theButtons = buttons;               // Store array handle at outer scope
        values = GetButtonValues(buttons);  // Get array of button values

        // Set up the dialog ready to be shown
        userValueDialog->Values = values;
        userValueDialog->LowerLimit = euroUserMinimum;
        userValueDialog->UpperLimit = euroUserMaximum;
        userValueDialog->SetLabelText(euroUserMinimum, euroUserMaximum);
    }
    // Check if the button is in the euroStars group box
    else if(euroStars->Controls->Contains(contextButton))
    {
        // The button is in the Stars group...
        array<Button^>^ buttons = { euroStar1, euroStar2 };
        theButtons = buttons;               // Store array handle at outer scope
        values = GetButtonValues(buttons);  // Get array of button values

        // Set up the dialog ready to be shown
        userValueDialog->Values = values;
        userValueDialog->LowerLimit = euroStarsUserMinimum;
        userValueDialog->UpperLimit = euroStarsUserMaximum;
        userValueDialog->SetLabelText(euroStarsUserMinimum, euroStarsUserMaximum);
    }
}
```