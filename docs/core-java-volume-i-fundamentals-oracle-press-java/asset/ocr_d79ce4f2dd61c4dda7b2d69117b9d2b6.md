# **TIP:**

You can use both plain and HTML text in buttons, labels, and menu items. I don’t recommend HTML in buttons—it interferes with the look-and-feel. But HTML in labels can be very effective. Simply surround the label string with `<html>. . .</html>`, like this:

```
```java
label = new JLabel("<html><b>Required</b> entry:</html>");
```
```

Note that the first component with an HTML label may take some time to be displayed because the rather complex HTML rendering code must be loaded.

Labels can be positioned inside a container like any other component. This means you can use the techniques you have seen before to place your labels where you need them.

# **javax.swing.JLabel 1.2**

+   - `JLabel(String text)`
+   - `JLabel(Icon icon)`
+   - `JLabel(String text, int align)`
+   - `JLabel(String text, Icon icon, int align)`
+   
+     constructs a label. The align parameter is one of the `SwingConstants` constants `LEFT` (default), `CENTER`, or `RIGHT`.
+   
+   - `String getText()`
+   - `void setText(String text)`
+   
+     gets or sets the text of this label.
+   
+   - `Icon getIcon()`
+   - `void setIcon(Icon icon)`