# TABLE D-12:

| PROPERTY | PURPOSE |
| --- | --- |
| Grid.Column | Sets the Grid cell where the splitter starts. For horizontal splitters, set this to 0. |
| Grid.ColumnSpan | For a horizontal splitter, set this so the control spans all columns. |
| Grid.Row | Sets the Grid cell where the splitter starts. For vertical splitters, set this to 0. |
| Grid.RowSpan | For a vertical splitter, set this so the control spans all rows. |
| HorizontalAlignment | For a vertical splitter, determines which side of its column the splitter sticks to and adjusts. |
| ShowsPreview | Determines whether the control resizes the Grid's rows or columns when you drag it, or only shows a preview by displaying a gray version of the GridSplit moving. If ShowsPreview is False, the control resizes the rows or columns. If ShowsPreview is True, the control displays the gray splitter and resizes the rows or columns when you release the mouse. (A preview is more efficient if the contents of the rows or columns take a long time to redraw) |
| VerticalAlignment | For a horizontal splitter, determines which side of its column the splitter sticks to and adjusts.

Usually the Grid and its controls can rearrange themselves when the user drags the GridSplitter, but the following events let you take action during the drag if you must (see Table D13).

# TABLE D-13: Key Events for GridSplitter

| EVENT | PURPOSE |
| --- | --- |
| DragCompleted | Occurs when the user has finished dragging the control. |
| DragDelta | Occurs when the user has moved the splitter during a drag. |
| DragStarted | Occurs when the user has started dragging the control.

# EXAMPLE Using GridSplitter

The following code creates a Grid with three rows and columns. It places GridSplitters inside the middle Grid cell. The first splitter has HorizontalAlignment set to Left so it lets the user adjust the left and middle columns. The second splitter has HorizontalAlignment set to Right so it lets the user adjust the middle and right columns.

```
<Grid>
  <Grid.ColumnDefinitions>
```