| class javafx.scene.layout.Pane |
|---|
| • `ObservableList<Node> getChildren()`<br>yields a mutable list of all children of this pane. |

| javafx.scene.shape.Shape |
|---|
| • `void setStroke(Paint value)`<br>sets the paint for drawing the boundary of this shape, or in the case of Line, Polyline, and Path, the shape itself.<br><br>• `void setFill(Paint value)`<br>sets the paint for drawing the interior of this shape. |

# 13.2.3 Text and Images

The “Not a Hello World” program at the beginning of this chapter displayed a string in the “System” font at its default size. Often, you will want to show your text in a different font. Use one of the static `Font.font` methods to obtain the font, and then call the `setFont` method on the `Text` object to set the font.

```
message.setFont(Font.font("Times New Roman", 36));
```

This Font factory method makes a font object representing the font with the given family name and point size. You can specify a bold and italic version by calling

```
Font.font("Times New Roman", FontWeight.BOLD, FontPosture.ITALIC, 36);
```

Fonts for the family names

+   - System
+   - Serif
+   - SansSerif
+   - Monospaced

are always available. The JDK ships with three font families:

+   - Lucida Bright
+   - Lucida Sans
+   - Lucida Sans Typewriter

The static method `Font.getFamilies` yields a list of all available family names.