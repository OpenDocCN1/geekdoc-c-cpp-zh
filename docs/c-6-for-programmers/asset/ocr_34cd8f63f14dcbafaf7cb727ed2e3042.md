BankUIForm (part of the BankLibrary project with this chapter’s examples) contains four Label1s and four TextBoxes. Methods ClearTextBoxes (lines 22–30), SetTextBoxValues (lines 33–51) and GetTextBoxValues (lines 54–59) clear, set the text in and get the text from the TextBoxes, respectively. Using visual inheritance—presented in Section 15.13—you can extend this class to create the GUIs for several examples in this chapter. Recall that to reuse class BankUIForm, you must compile the GUI into a class library, then add a reference to the new class library’s DLL in each project that will reuse it (see Section 15.13).

```
// Fig. 17.2: BankUIForm.cs
// A reusable Windows Form for the examples in this chapter.
using System;
using System.Windows.Forms;

namespace BankLibrary
{
    public partial class BankUIForm : Form
    {
        protected int TextBoxCount { get; set; } = 4; // number of TextBoxes

        // enumeration constants specify TextBox indices
        public enum TextBoxIndices { Account, First, Last, Balance}

        // parameterless constructor
        public BankUIForm()
        {
            InitializeComponent();
        }

        // clear all TextBoxes
        public void ClearTextBoxes()
        {
            // iterate through every control on form
            foreach (Control guiControl in Controls)
            {
                // if Control is TextBox, clear it
                (guiControl as TextBox)?.Clear();
            }
        }

        // set text box values to string-array values
        public void SetTextBoxValues(string[] values)
        {
            // determine whether string array has correct length
            if (values.Length != TextBoxCount)
            {
                // throw exception if not correct length
                throw (new ArgumentException(
                    $"There must be {TextBoxCount} strings in the array",
                    nameof(values)));
            }
```

Fig. 17.2 | A reusable Windows Form for the examples in this chapter’s apps. (Part 1 of 2.)