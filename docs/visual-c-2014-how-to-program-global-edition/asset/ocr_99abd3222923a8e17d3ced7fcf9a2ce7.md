# 14.7 CheckBoxes and RadioButtons 609

| | | |
|---|---||
| 11 | Bold and Italic |
| 01 | Bold |
| 10 | Italic |

This is a simple example. The advantages of using bitwise operators to combine FontStyle values become more evident when we consider that there are five FontStyle values (Bold, Italic, Regular, Strikethout and Underline), resulting in 16 FontStyle combinations. Using bitwise operators to combine font styles greatly reduces the amount of code required to check all possible font combinations.

In 14.26, we need to set the FontStyle so that the text appears in bold if it was not originally, and vice versa. Line 23 uses the bitwise logical OR operator to do this. Outputlabel.Font.FontStyle is bold, then the resulting style is not bold. If the text is originally italic, the resulting style is bold and italic, rather than just bold. The same applies for FontStyle.Italic in line 32.

If we didn't use operators to compute FontStyle elements, we'd have to test for the current style and change it accordingly. In boCheckBox_CheckedChanged, we would test for the regular style and make bold, test for the bold style and make regular, test for the italic style and make it bold and test for the italic bold and make it italic. This is cumbersome, for every new style we add, we double the number of combinations. Adding a Checkbox for underline would require testing eight additional styles. Adding a Checkbox for strikethout would require sixteen additional styles.

# 14.7.3 RadioButtons

Radio buttons (defined with class radioButton) are similar to CheckBoxes in that they also have two states—selected and not selected (also deselected). However, RadioButtons appear as a group, in which only one RadioButton can be selected at a time. Selecting one RadioButton in the group forces all the others to be deselected. Therefore, RadioButtons are used to represent a set of mutually exclusive options (i.e., a set in which multiple options cannot be selected at the same time).

> Look-and-Feel Observation 14.4
Use RadioButtons when the user should choose only one option in a group. Use CheckBoxes when the user should be able to choose multiple options in a group.

All RadioButtons added in a container are in the same group. To divide RadioButtons into several groups, they must be added to separate containers, such as GroupBoxes or Panels. Radio's common properties and a common event are listed in 14.27.

![](bbox=[0.147, 0.656, 0.21, 0.696])

| Common Properties Description|Checked Indicates whether the RadioButton is checked. |Text Specifies the RadioButton's text.|

Fig. 14.27 | RadioButton properties and an event. (Part I of 2.)