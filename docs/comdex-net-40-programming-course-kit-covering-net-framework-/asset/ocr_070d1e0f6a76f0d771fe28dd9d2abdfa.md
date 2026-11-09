![](bbox=[0.387, 0.137, 0.635, 0.228])

Fig.VB-4.46

After learning about the SaveFileDialog control, let’s learn about the FontDialog control.

# Using the FontDialog Control

The FontDialog control allows you to provide users the facility to work with the Font dialog box. In the Font dialog box, a user can select a font, font size, and font color. Users can also use the Font dialog box to add textual effects, such as underlining the text and applying shadows to the text. The FontDialog class, which is placed inside the System.Windows.Forms namespace, provides the functionality for the FontDialog control. Table 4.18 lists the noteworthy properties of the FontDialog class:

| Property | Description |
|---|---|
| AllowVerticalFonts | Returns or sets a value that indicates whether only the horizontal fonts or both vertical and horizontal fonts appear in the dialog box. |
| Color | Returns or sets a Color object that represents the font color selected in the dialog box. |
| FixedPitchOnly | Returns or sets a value that indicates whether only fixed-pitch fonts can be selected in the dialog box. Fixed-pitch fonts are those fonts in which all the characters have the same width. |
| Font | Returns or sets a Font object that represents the font selected in the dialog box. |
| FontMustExist | Returns or sets a value that indicates whether an error message is displayed to the users if a user specifies a non-existent font or font style. |
| MaxSize | Returns or sets the maximum font size that a user can specify. |
| MinSize | Returns or sets the minimum font size that a user can specify. The default value for this property is zero. |
| ShowApply | Returns or sets a value that indicates whether an Apply button appears in the dialog box or not. |
| ShowColor | Returns or sets a value that indicates whether the dialog box provides the facility to select a font color or not. |
| ShowEffects | Returns or sets a value that indicates whether the dialog box provides the facility to select textual effects, such as strikethout and underline. |
| ShowHelp | Returns or sets a value that indicates whether a Help button appears in the dialog box or not. |

Table 4.19 lists a noteworthy event of the FontDialog class:

| Event | Description |
|---|---|
| Apply | Occurs when a user clicks the Apply button in the Font dialog box |

Perform the following steps to use the FontDialog control in a Windows Forms application:

+   1. *Start* Visual Studio 2010.