When the user clicks a mouse button, three events are generated: “mouse pressed,” when the mouse button is first pressed; “mouse released,” when the mouse button is released; and, finally, “mouse clicked,” after pressing and releasing the button. In our example, we capture mouse presses because we don’t want to delay the visual feedback until the mouse button is released.

By using the getX and getY methods on the MouseEvent argument, you can obtain the x- and y-coordinates of the mouse pointer.

```
```java
root.setOnMousePressed(event ->
{
    double x = event.getX();
    double y = event.getY();
    Circle dot = new Circle(x, y, RADIUS);
    root.getChildren().add(dot);
});
```
```

To distinguish between single, double, and triple (!) clicks, use the getClickCount method. To find out which button was pressed, call the getButton method:

```
```java
if (event.getButton() == MouseButton.SECONDARY) . . . // right click
```
```

Some user interface designers inflict mouse click and keyboard modifier combinations, such as Control+Shift+click, on their users. We find this practice reprehensible, but if you disagree, call one of the following methods:

+   isShiftDown
+   isControlDown
+   isAltDown
+   isMetaDown
+   isShortcutDown

The Alt key is labeled Option (⌥) on the Mac. The Meta key is the Windows or Command (⌘) key. The isShortcutDown method tests for the preferred modifier of the platform—Control on Linux and Windows, Meta on the Mac.

As the mouse moves, a steady stream of mouse movement events are generated. Any node can ask to be notified when the mouse passes over it. Our test application traps mouse motion events to change the cursor to a different shape (a crosshair) when it is over a dot:

```
```java
dot.setOnMouseEntered(event -> scene.setCursor(Cursor.CROSSHAIR));
dot.setOnMouseExited(event -> scene.setCursor(Cursor.DEFAULT));
```
```

Table 10.3 lists the available cursors.