# Introduction to Programming and Problem-Solving Using Scala

contents. they are then laid out rows, forming new rows as needed. The TilePane works like the FlowPane other than how things are sized.

Note that the BorderPane is set to be the root of the Scene. As was mentioned before, this causes it to be bound to the size of the window, so that the controls adjust when the window size is changed. This will not happen by default if you use content.

The GridPane is a bit more complex than the panes in the previous example, so we give it its own. The following code shows how a GridPane could be used to lay out a GUI for a basic calculator.

# Listing 11.18: GridPane.scala

```
import scalax.Includes._nimport scalax.scene.Scene
import scalax.application.JFXApp
import scalax.scene.control.*
import scalax.scene.layout.GridPane
import scalax.scene.layout.Priority

val app = new JFXApp {
stage = new JFXApp.PrimaryStage {
title = "GridPane"
scene = new Scene(300,300) {
val gridPane = new GridPane
for (i <- 1 to 9) {
val button = new Button(i.toString)
gridPane.children += button
gridPane.setColumnIndex(button, (i-1)%3)
gridPane.setRowIndex(button, (i-1)/3+1)
gridPane.setHgrow(button, Priority.Always)
gridPane.setVgrow(button, Priority.Always)
button.maxWidth = Int.MaxValue
button.maxHeight = Int.MaxValue
}
val textField = new TextField
gridPane.children += textField
val zeroButton = new Button("0")
gridPane.children += zeroButton
gridPane.setConstraints(textField,0,0,4,1)
gridPane.setVgrow(zeroButton,0,4,2)
zeroButton.maxWidth = Int.MaxValue
zeroButton.maxHeight = Int.MaxValue
val periodButton = new Button(".*")
gridPane.children += periodButton
gridPane.setConstraints(periodButton,2,4)
gridPane.setVgrow(periodButton, Priority.Always)
periodButton.maxWidth = Int.MaxValue
periodButton.maxHeight = Int.MaxValue
val plusButton = new Button("+")
ngridPane.children += plusButton
gridPane.setConstraints(plusButton,3,1)
gridPane.setHgrow(plusButton, Priority.Always)
plusButton.maxWidth = Int.MaxValue
plusButton.maxHeight = Int.MaxValue
val minusButton = new Button("-")
}}
```