# 11.7 Layout and Panes

While you can use bindings to make things move around when you change the size of a window, this really is not the way to build complex user interfaces. The proper way to make complex interfaces in ScalaFX is with layouts and panes. Most of these are in the scalafx.scene.layout package, but some are scalafx.scene.control. The ones in control produce simple layouts that do not interact with the user. Using either of these, you can create complex displays by nesting them inside one another. The panes themselves are Nodes, so you can add them to one another in the same way that you might add a Button. Each has its own rules for how the elements inside it change size when the whole thing changes.

# 11.7.1 scalafx.scene.layout Panes

The following list describes the types provided in the scalafx.scene.layout package in alphabetical order.

+   **AnchorPane** — This pane allows you to set the location of contents inside it to the location of this pane. You can call methods like AnchorPane.setAnchor(child:Node, value:Double) to specify where a child should appear in the AnchorPane. Items can be anchored to more than one edge.
**BorderPane** — Arranges elements in five different regions: top, bottom, left, right, and center. The elements at the top and bottom span the full width of the pane and the left and right elements take the remaining space in height and as much as they need in. The center element gets whatever is left over.
**FlowPane** — This pane places the contents one after another with a horizontal or vertical orientation, giving each as much space as it wants. When it runs out of space it starts a new row or column, based on the orientation.
**GridPane** — Arranges elements in a flexible grid. The elements can be placed at any row and column, and they are allowed to cover multiple rows and/columns. The rows and columns are sized to accommodate the elements that they are in.
**HBox** — Arranges elements horizontally to one another.
**StackPane** — St elements on top of one another in the same area of the screen so they overlap.
**TilePane** — Arranges the elements in a grid of uniform “tiles”. The contents are arranged across each row first. Tile sizes are determined by the contents by default.
**VBox** — Arranges the elements vertically below the one before it.

To help illustrate this work, the following code creates a GUI that has a BorderPane as the primary contents, with a VBox on the left, a FlowPane on bottom, a StackPane on the right, and a TilePane in the center. In each of these we add a Button, a Label, a TextField, a TextArea, a ComboBox, and a Slider.