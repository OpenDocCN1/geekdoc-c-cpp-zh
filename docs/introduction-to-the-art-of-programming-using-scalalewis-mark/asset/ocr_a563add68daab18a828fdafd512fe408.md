+   - Reactions are given as partial functions. These look like the case portion of a match.
+   - GUI actions can be made faster and easier for the user using mnemonics that attach keystrokes to them.

+   - The FileChooser type provides a standard file selection dialog box.
+   - The Table component is an easy to use method of displaying a grid of data.

+   - There are a number of different actions that can occur with Tables that you might want to react to.
+   - To have complete control over a Table you would need to write a new TableModel. You can have the ability to resize Tables by simply creating new instances of DefaultTableModel with the modified size.

# 11.7.2 Self-Directed Study

Enter the following statements into the REPL and see what they do. Some might produce errors. You should try to figure out why. Try some variations to make sure you understand what is going on.

```
scala> import scala.swing._
scala> import event._
val frame = new Frame {
  | title = "Small"
  | contents = new Label("A Label")
  | }
scala> frame.visible = true
scala> frame.size = new Dimension(500,500)
scala> frame.dispose
scala> val frame = new Frame {
  | title = "Large"
  | contents = new Label("Another Label")
  | size = new Dimension(600,600)
  | }
scala> frame.visible = true
scala> frame.dispose
val frame = new Frame {
  | title = "4 Buttons"
  | contents = new GridPanel(1,4) {
  | for(i <- 1 to 4) contents += Button("b"+i)(println(i))
  | }
  | }
scala> frame.visible = true
scala> frame.dispose
scala> val frame = new Frame {
  | title = "Append Numbers"
  | val field = new TextField
  | contents = new BorderPanel {
  | layout += field -> BorderPanel.Position.North
  | layout += new GridPanel(1,10) {
  | for(i <- 1 to 10) {
  | val str = (i%10).toString
  | contents += Button(str)(field.text += str)
  | }
```