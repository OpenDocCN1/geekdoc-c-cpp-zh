Next, the code places a Viewbox centered inside the Grid. Recall that a Viewbox's purpose is to stretch its single child in various ways.

If the routine's margin parameter is null, the code should display the window at its normal scale, it sets the Viewbox's Stretch property to None.

If the routine's margin parameter is not null, the code should enlarge the window. It sets the Viewbox's Margin property to the margin parameter the Viewbox expands to fill the Grid except for the margin. It also sets the Viewbox's Stretch property to Uniform so it enlarges its child control as much as possible without changing its aspect ratio (ratio of width to height).

Next, the code makes a Visualbrush that contains an image of the window that it should print.
It makes a Rectangle with the same size as the window, fills the Rectangle with the VisualBrush, and places the Rectangle inside the Viewbox. The Viewbox stretches the Rectangle if appropriate.

Next, the code calls the Grid's Arrange method. The Grid recursively arranges its child and renders them. If you omit this call, the code runs, but the printout is blank.

Finally, the code calls the PrintDialog's PrintVisual method to print the Grid and its contents
If the user clicks on the dialog's Preferences button and changes the printer's orientation to landscape, the PrintDialog's PrintableAreaWidth and PrintableAreaHeight automatically switches so the controls are arranged properly.

Figure 17-4 shows the result when the program's window is stretched and printed using the Microsoft XPS Document Writer with preferences set to landscape orientation and displayed in XPS Viewer.

![](bbox=[0.503, 0.391, 0.896, 0.7])

# PRINTING CODE-GENERATED OUTPUT

The PrintDialog object's PrintVisual method is easy to use, and can produce nicely scaled and centered results. It assumes that you are only printing one page at a time, however. If you want to print a longer document, you'll need to call PrintVisual once for each page, and it will produce one print job for each page. This isn't an ideal solution. Frequently there's a better way to produce multiple-page printouts.