![](bbox=[0.22, 0.12, 0.66, 0.29])

The `ListBox` on the left lists the students in the `Students` table. When you click on a student, the controls in the middle display the student's address and phone number, and the `ListBox` on the right displays the corresponding test score data from the `TestScores` table.

If you modify any of the student values in the middle, the controls automatically update the corresponding `ADO.NET` objects. If you use the Data menu's "Save Changes" command, the program writes those changes back into the database. (This example doesn't provide a way to add or delete students, or to add or modify a student's test scores.)

The database has a third table named `States` that lists the U.S. states (plus Washington, DC) and their abbreviations. The program uses this table as a lookup table. The `Students` table contains each student's state as an abbreviation. When it displays that value, the `ComboBox` in the middle of the window uses the `States` table to convert the abbreviation into the state's full name.

# TRANSFORMATIONS

A *transformation* alters an object's geometry before it is drawn. Different kinds of transformations stretch, rotate, squash, skew, and move an object.

WPF provides four basic kinds of transformations represented by the following XAML elements:

+   - `RotateTransform` — This transformation rotates an object. The `Angle` property determines the number of degrees by which the object is rotated clockwise.
+   - `ScaleTransform` — This transformation scales the object vertically and horizontally. The `ScaleX` and `ScaleY` properties determine the horizontal and vertical scale factors respectively.
+   - `SkewTransform` — This transformation skews the object by rotating its X and Y axes through an angle given by the `AngleX` and `AngleY` properties.
+   - `TranslateTransform` — This transformation moves the object. The `X` and `Y` properties determine how far the object is moved horizontally and vertically.

To apply a transformation to an object, give that object a `LayoutTransform` or `RenderTransform` property element that contains one of the four basic transformations. When you use a `LayoutTransform`, WPF modifies the control before it arranges the controls. When you use a `RenderTransform`, WPF arranges the controls first and then modifies the control.