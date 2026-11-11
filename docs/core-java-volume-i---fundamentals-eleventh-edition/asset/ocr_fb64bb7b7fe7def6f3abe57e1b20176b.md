# javafx.scene.text.Font

+   - `static Font.font(double size)`
+   - `static Font.font(String family)`
+   - `static Font.font(String family, double size)`
+   - `static Font.font(String family, FontWeight weight, double size)`
+   - `static Font.font(String family, FontPosture posture, double size)`
+   - `static Font.font(String family, FontWeight weight, FontPosture posture, double size)`
+   
+   obtains a font with the given family name (or "System"), weight and posture (or FontWeight.NORMAL and FontPosture.REGULAR), and point size.

# javafx.scene.text.Text

+   - `void setFont(Font value)`
+     sets this text to the given font.
+   - `double getX()`
+   - `double getY()`
+     gets the x- and y-position of the baseline of this text node.

# javafx.scene.Node

+   - `Bounds getBoundsInParent()`
+     gets the bounds of this node after applying any strokes, clips, effects, and transformations.
+   - `void relocate(double x, double y)`
+     relocates this node so that its top left corner falls on the given x- and y-values.

# javafx.geometry.Bounds

+   - `double getMinX()`
+   - `double getMinY()`
+   - `double getMaxX()`
+   - `double getMaxY()`
+     gets the smallest or largest x- and y-value of these bounds.
+   - `double getWidth()`
+   - `double getHeight()`
+     gets the width and height of these bounds.