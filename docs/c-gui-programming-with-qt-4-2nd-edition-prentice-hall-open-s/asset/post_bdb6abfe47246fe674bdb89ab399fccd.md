
| Type | QDial |
| --- | --- |
| | Instances of a given class, including subclasses |
| Class | .QDial | Instances of a given class, excluding subclasses |
| ID | QDial#ageDial | Widgets with the given object name |
| Qt property | QDial[y="0"] | Widgets with certain properties set to values |
| Child | QFrame > QDial | Widgets that are direct children of the widgets |
| Descendant | QFrame QDial | Widgets that are descendants of the given widgets |

```
QPushButton[text="OK"] {
  color: green;
}
```

```
QPushButton[text="Cancel"] {
  color: red;
}
```

This selector syntax works for any Qt property, although we must bear in mind that style sheets don't notice when a property changes behind their backs. Selectors can be combined in various ways; for example, to select all QPushButtons called "okButton" whose x and y properties are 0 and that are direct children of a QFrame called "frame", we can write

```
QFrame#frame > QPushButton[x="0"][y="0"]#okButton {
  ..
```

In an application that presents large forms with lots of line editors and comboboxes, such as those used by various bureaucracies, it is common to use a yellow background color for mandatory fields. Let's suppose we want to apply this convention to our application. First, we would start with this style sheet:

```
*[mandatory="true"] {
  background-color: yellow;
}
```

Although there is no mandatoryField property defined anywhere in Qt, we can easily create one by calling QObject::setProperty(). Starting with Qt 4.2, setting the value of a non-existent property dynamically creates that property. For example:

```
nameLineEdit->setProperty("mandatoryField", true);
genderComboBox->setProperty("mandatoryField", true);
ageSpinBox->setProperty("mandatoryField", true);
```

Style sheets are not only useful for controlling colors. They also let us perform various adjustments to the size and position of widget elements. For example, the following rules can be used to increase the size of checkboxes and radio button indicators to 20 x 20 pixels, and ensure that there are 8 pixels between the indicator and the associated text:

```
QCheckBox::indicator, QRadioButton::indicator {
  width: 20px;
  height: 20px;
}
QCheckBox, QRadioButton {
  spacing: 8px;
```

Notice the selector syntax for the first rule. Had we written only QCheckBox instead of QCheckBox::indicator, we would have specified the dimensions of the entire widget instead of those of the indicator. The first rule is illustrated in Figure 19.3.

# Figure 19.3. Setting a QCheckBox's indicator size

![](img/5a524abdf0b0d58fa99d30abb4463611_712_0.png)

Subcontrols such as ::indicator can be styled in much the same way as widgets.

# Figure 19.4. The most common customizable subcontrols

| Subcontrol | Description |
| --- | --- |
| ::indicator | A checkbox, radio button, changeable menu item, or changeable group box's indicator |
| ::menu-indicator | A push button's menu indicator |
| ::item | A menu, menu bar, or status bar item |
| ::up-button | A spin box or scroll bar's up button |
| ::down-button | A spin box or scroll bar's down button |
| ::up-arrow | A spin box, scroll bar, or header view's arrow |
| ::downarrow | A spin box, scroll bar, header view, or combobox's down arrow |
| ::drop-down | A combobox's drop-down arrow |
| ::title | A group box's title |

In addition to subcontrols, a style sheet can refer to specific widget states. For example, we may want to render the checkbox's text in white when the mouse hovers over it by specifying the :hover state:

```
QCheckBox:hover {
  color: white;
}
```

States are signified by using a single colon: whereas subcontrols are signified by using two colons. We can list several states one after another, each separated by a colon. In such cases, the rule will apply only when the widget is in all the specified states. For example, the following rule is applied only if the mouse is hovering over a checked checkbox:

```
QCheckBox:checked:hover {
  color: white;
}
```

If we want the rule to apply when any of the states is true, we can use multiple selectors, using commas to separate them:

```
QCheckBox:hover, QCheckBox:checked {
  color: white;
}
```

Logical negation is achieved by using an exclamation mark:

```
QCheckBox::!checked {
  color: blue;
}
```

States can be combined with subcontrols:

```
QComboBox::drop-down:hover {
  image: url(:images/downarrow_bright.png);
}
```

Figure 19.5 lists the style sheets that are available.

> Figure 19.5. Some of the widget states accessible to style sheets

| State | Description |
| --- | --- |
| :disabled | The widget is disabled |
| :enabled | The widget is enabled |
| :focus | The widget has input focus |
| :hover | The mouse is hovering over the widget |
| :pressed | The widget is being pressed using the mouse |
| :checked | The button is checked |
| :unchecked | The button is unchecked |
| :indeterminate | The button is partially checked |
| :open | The widget is in an open or expanded state |
| :closed | The widget is in a closed or collapsed state |
| :on | The widget is "on" |
| :off | The widget is "off" |

Style sheets can also be used together with other techniques to perform more complex customizations. For example, suppose we want to position a tiny "erase" button inside a QLineEdit, to the right of the Qt text. This involves creating an EraseButton class, and placing it on top of the QLineEdit (e.g., using layouts), but also reserving some space for the button, so that the typed-in text cannot collide with the erase button. By subclassing QStyle would be inconvenient, because we would have to subclass every style in Qt that might be used by the application (QWindowsStyle, QPlastiqueStyle, etc.). Using style sheets, the following rule does the trick:

```
QLineEdit {
padding: 15px;
}
```

The padding property allows us to specify the top, right, bottom, and left padding. For example, the following rule shows the padding of the QLineEdit:

```
QLineEdit {
  padding: 0px;
}
```

Like most widgets are customizable by style sheets, the model depicted in Figure 19.6 shows:

1. The contents rectangle is the innermost rectangle.
2. The padding rectangle encloses the contents.
3. The border rectangle surrounds the padding.
4. The margin rectangle is the outermost rectangle.

# Figure 19.6. The CSS model

![](img/5a524abdf0b0d58fa99d30abb4463611_716_0.png)

We will now present a style sheet that called Candy. Figure 19.7 shows the styled widgets. The entire style sheet is available as qss/candy.qss supplied with the book.

# Figure 19.7. Widgets in Candy

![](img/5a524abdf0b0d58fa99d30abb4463611_716_1.png)

The dialog itself has a background image set by the following rule:

```
Dialog {
    background-image: url(:images/background.png);
}
```

The following rule sets the color and font attributes for QLabels:

```
QLabel {
    font: 9pt;
}
```

The next rule defines the look of the dialog's QLineEdit and of its ListView:

```
QLineEdit,
QListView {
  color: rgb(0, 0, 63);
  background-color: rgb(255, 255, 241);
  selection-color: white;
  selection-background-color: rgb(191, 31, 127);
  border: 2px groove gray;
  border-radius: 10px;
  padding: 2px 4px;
}
```

To make the QLineEdit and QListView really stand out, we have specified custom foreground and background colors for normal and selected text. In addition, we have specified a gray 2-pixel width "grooved" border with the border attribute. Instead of using border we could have set border-width, border-style, and border-color individually. We can round a border's corners by specifying a border-radius, and we have done so here using a radius of 10 pixels. Figure 19.8 provides a schematic representation of the effects of the widgets' border and padding attributes. To ensure that the widget's contents don't collide with the border's rounded corners, we specify an internal padding of 2 pixels vertically and 4 pixels horizontally. For QListView, the vertical padding doesn't look quite right, so we override it as follows:

```
QListView {
  padding: 5px 4px;
}
```

# Figure 19.8. Structure of a QLineEdit

![](img/5a524abdf0b0d58fa99d30abb4463611_717_0.png)
