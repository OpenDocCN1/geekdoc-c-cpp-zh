another 1, the list will decrease to the four elements that begin with Holl. If you then type an o, the list will contain only the entry Holloway.

The AutoCompleteMode has two other modes. The Append mode does not automatically present a drop-down, but instead appends the rest of the closest matching entry to the text in the Textbox or ComboBox, and highlights the untyped characters. This allows the closest matching entry to be placed in the text area without the user explicitly selecting an entry.

The SuggestAppend mode combines Suggest and Append. The current best match is displayed in the text area, and the drop-down with other possibilities is automatically displayed. This mode is the one most like IntelliSense.

You can also set the list of items to be included in the autocompletion list at runtime, which is the most common usage scenario. A list of items from a database table would typically be loaded for autocompletion. Here is typical code to create a list of items and attach the list to a ComboBox:

```
Dim autoCompleteStringCollection1 As New AutoCompleteStringCollection
Dim nReturn As Integer
nReturn = autoCompleteStringCollection1.Add("Holder")
nReturn = autoCompleteStringCollection1.Add("Holland")
nReturn = autoCompleteStringCollection1.Add("Hollis")
nReturn = autoCompleteStringCollection1.Add("Holloway")
ComboBox1.AutoCompleteCustomSource = autoCompleteStringCollection1
```

Code snippet from AutoComplete

For this sample to work properly, the ComboBox control's AutoCompleteSource property must be set to CustomSource.

Several built-in lists are available for use with autocompletion. Instead of setting AutoCompleteSource to CustomSource, you can set it to sources such as files in the file system, or URLs recently used in Internet Explorer. See the documentation for AutoCompleteSource for additional options; or, if you are using AutoCompleteSource in code, IntelliSense will show the options available.

# MaskedTextbox Control

The MaskedTextbox control allows entry of information that conforms to a “mask” which determines what is and is not valid in each character position. You can set the Mask property in the Properties window, but you can also click the smart tag (right-pointing arrow) on the right side of the MaskedTextbox. In both cases, you can either construct a mask manually or select one of the commonly used masks from a list.

If you want to create your own mask, you need to design it based on the set of formatting characters described in Table 14-4.

# TABLE 14-4: Mask Characters Available in the MaskedTextBox Control

| MASK CHARACTER | DESCRIPTION |
|---|---|
| # | Digit placeholder |
| . | Decimal placeholder. The actual character used is the one specified as the decimal placeholder in your international settings. This character is treated as a literal for masking purposes. |
| , | Thousands separator. The actual character used is the one specified as the thousands separator in your international settings. This character is treated as a literal for masking purposes. |
| : | Time separator. The actual character used is the one specified as the time separator in your international settings. This character is treated as a literal for masking purposes. |
| / | Date separator. The actual character used is the one specified as the date separator in your international settings. This character is treated as a literal for masking purposes. |