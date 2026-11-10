# ### 12.3.2 Checkboxes and Radio Buttons

To create a checkbox or radio button, the corresponding program/dictionary field should be of type `C` and length `1`. When the checkbox or radio button is selected, the corresponding program data object will be passed `X`. We can identify if the checkbox or radio button is selected by checking the corresponding program field for `X` or a space.

In the SCREEN PAINTER: DICT./PROGRAM FIELDS window, select the checkbox (ChkB) or radio button (RadB) option under the Copy As column (see Figure 12.20). These options will be enabled only if the field is of TYPE C and LENGTH 1.

![](bbox=[0.14, 0.35, 0.85, 0.62])

**Figure 12.20** Copying Checkbox/Radio Button

The checkbox and radio button elements can also be created by selecting them from the element palette. The radio buttons should be grouped so that only one of the buttons in the group can be selected at a time. To group the radio buttons, select all the buttons that should be part of the group (by holding the `Ctrl` key and clicking each element), right-click, and select RADIO BUTTON GROUP • DEFINE from the context menu, as shown in Figure 12.21.