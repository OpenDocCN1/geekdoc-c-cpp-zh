# Popular Properties

You'll learn about key control properties as you go along, but for now Table 2-1 summarizes some of the most useful properties. Note that not all controls have every property. For example, a `Button` cannot display a border (or it always displays a border, depending on your point of view) so it has no `BorderStyle` property.

TABLE 2-1

| PROPERTY | PURPOSE |
|---|---|
| `Anchor` | Determines how the control sizes itself to use the available space. This property is described further in Lesson 3. |
| `AutoSize` | Determines whether the control automatically resizes itself to fit its contents. This can be `True` or `False`. By default, `Labels` are born with `AutoSize = True`. |
| `BackColor` | Determines the control's background color. |
| `BackgroundImage` | Determines the image that the control displays. |
| `BorderStyle` | Determines whether the control displays a border. This can be `None`, `FixedSingle`, or `Fixed3D`. |
| `Dock` | Determines how the control sizes itself to use the available space. This property is described further in Lesson 3. |
| `Enabled` | Determines whether the control will interact with the user. Many controls display a special appearance when disabled such as being grayed out. This can be `True` or `False`. |
| `Font` | Determines the font that the control uses to display text. |
| `ForeColor` | Determines the control's foreground color. For controls that display text, this is usually the text's color. |
| `Image` | Determines the image that the control displays. (Some controls have `Image`, others have `BackgroundImage`, a few have both, and many cannot display any image. No one said this was completely consistent!) |
| `Items` | For controls such as `ListBox` and `ComboBox`, this is the list of items that the user can select. |
| `Location` | Gives the control's location in pixels from the upper-left corner of whatever it is in (for now, assume it's in the form). `Location` includes X and Y sub-properties. For example, the value (10, 20) means the control is 10 pixels from the form's left edge and 20 pixels from its top edge. |
| `Name` | Gives the control a name that your code can use to refer to it later. You should always give a good name to any control that you will refer to in code. |