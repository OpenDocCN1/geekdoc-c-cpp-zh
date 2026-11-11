| javax.swing.JTextArea 1.2 *(Continued)* |
|---|
| • `void setWrapStyleWord(boolean word)`<br>If word is true, long lines are wrapped at word boundaries. If it is false, long lines are broken without taking word boundaries into account.<br><br>• `void setTabSize(int c)`<br>sets tab stops every c columns. Note that the tabs aren’t converted to spaces but cause alignment with the next tab stop. |

| javax.swing.JScrollPane 1.2 |
|---|
| • `JScrollPane(Component c)`<br>creates a scroll pane that displays the content of the specified component. Scrollbars are supplied when the component is larger than the view. |

# 11.4 Choice Components

You now know how to collect text input from users, but there are many occasions where you would rather give users a finite set of choices than have them enter the data in a text component. Using a set of buttons or a list of items tells your users what choices you have. (It also saves you the trouble of error checking.) In this section, you will learn how to program checkboxes, radio buttons, lists of choices, and sliders.

# 11.4.1 Checkboxes

If you want to collect just a “yes” or “no” input, use a checkbox component. Checkboxes automatically come with labels that identify them. The user can check the box by clicking inside it and turn off the checkmark by clicking inside the box again. Pressing the space bar when the focus is in the checkbox also toggles the checkmark.

Figure 11.12 shows a simple program with two checkboxes, one for turning the italic attribute of a font on or off, and the other for boldface. Note that the second checkbox has focus, as indicated by the rectangle around the label. Each time the user clicks one of the checkboxes, the screen is refreshed, using the new font attributes.