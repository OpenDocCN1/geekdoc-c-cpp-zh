of error checking.) In this section, you will learn how to program checkboxes, radio buttons, lists of choices, and sliders.

# 11.4.1 Checkboxes

If you want to collect just a “yes” or “no” input, use a checkbox component. Checkboxes automatically come with labels that identify them. The user can check the box by clicking inside it and turn off the checkmark by clicking inside the box again. Pressing the space bar when the focus is in the checkbox also toggles the checkmark.

[Figure 11.12](#) shows a simple program with two checkboxes, one for turning the italic attribute of a font on or off, and the other for boldface. Note that the second checkbox has focus, as indicated by the rectangle around the label. Each time the user clicks one of the checkboxes, the screen is refreshed, using the new font attributes.

![](bbox=[0.272, 0.457, 0.729, 0.694])

**Figure 11.12** Checkboxes

Checkboxes need a label next to them to identify their purpose. Give the label text in the constructor:

```
```java
bold = new JCheckBox("Bold");
```
```

Use the setSelected method to turn a checkbox on or off. For example: