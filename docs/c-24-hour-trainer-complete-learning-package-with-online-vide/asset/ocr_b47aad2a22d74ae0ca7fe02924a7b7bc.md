# Background Color

+   - White
+   - Pink
+   - Light Green
+   - Light Blue

+   - Initially check the Text Color menu's Black choice and the Background Color menu's White choice.
+   - Give the Background Color menu items Images that display samples of the colors.
+   - Create the ToolStrip with buttons that duplicate the menu hierarchy. The ToolStrip should hold two ToolStripDropDownButtons.
+     - Name the first tool foreColorButton and make it display the text "A." Give it the items Black, Red, Green, and Blue. Each item should have the ForeColor property set to its color.
+     - Name the second tool backColorButton and make it initially display a white color sample. Give it the items White, Pink, Light Green, and Light Blue. Make each of these display an Image showing a sample of the color.
+   - Give the StatusStrip a ToolStripStatusLabel named colorLabel with Text = Text Colors.
+   - Add event handlers.
+     - Make the File menu's Exit item close the form.
+     - Make event handlers for each of the Text Color menu items.
+     - Make event handlers for each of the Background Color menu items.
+   - Make the tool strip Buttons use the corresponding menu items' event handlers.

# DUPLICATE CODE

As you will probably notice, this lesson's Try It includes event handlers that duplicate the same code with minor differences. In general, if large pieces of code do almost the same things with minor changes, then there's probably something wrong with the program's design.

In cases such as this, you should extract the common code into a method. You can use if, switch, and other C# statements to let the code take different actions for different situations, allowing one method to handle multiple situations.

Unfortunately, you don't know how to do any of that yet, but you will learn. Lesson 18 describes statements such as if and switch, and Lesson 20 explains how to write methods. Until then, you're stuck with some duplicate code.