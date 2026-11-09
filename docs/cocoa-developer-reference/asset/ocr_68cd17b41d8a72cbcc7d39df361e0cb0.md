Figure 13.15 shows the finished application. It has the following features:

+   - There are three independent columns of data showing values from the `running-apps` array.
+   - The table dividers can be moved.
+   - Rows can be selected by clicking on them, and there is an optional selection index used to return information about the number of the current selection.
+   - Columns can be sorted by clicking on each column header to select ascending or descending sorting.

The application has some limitations. It doesn’t auto-refresh the table; the array is loaded once at launch, and isn’t updated. In its basic state, it’s a display-only app. There are no features for starting and stopping apps, saving the list to a file, maintaining a log file, and so on.

But it’s doing a lot with very little code. And most of the intelligence is built into a controller object, coupled to the array and the table view via bindings.

# Figure 13.15

Filling a table view with bindings. Most of the active code is built into a controller object and runs automatically.

![](bbox=[0.169, 0.497, 0.725, 0.709])

# Adding a controller object

Figure 13.16 shows the project nib file. The table view automatically adds a surrounding scroll view. The default table view has two columns. Another column has been added by copying and pasting it. Each column’s name — the text string that appears in the divider, at the top of the header — is set in the Attributes pane in Inspector. The size pane sets the default width and optional width limits. Take some time to explore these features before continuing.