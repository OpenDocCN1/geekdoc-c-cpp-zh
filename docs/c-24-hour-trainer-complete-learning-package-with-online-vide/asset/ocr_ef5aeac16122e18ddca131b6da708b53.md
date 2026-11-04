# # TRY IT

In this Try It, you use event handlers to display color samples as the user adjusts red, green, and blue scrollbars.

Figure 4-4 shows the finished program in action. When you change a scrollbar’s value, the label to the right shows the color component’s new numeric value, and the large label on the far right shows a sample of the color with the selected red, green, and blue color components.

![](bbox=[0.146, 0.251, 0.437, 0.33])

FIGURE 4-4

# ## Lesson Requirements

In this lesson, you:

+   - Create the form shown in Figure 4-4. Arrange the controls and set their Anchor properties.
+   - Make an event handler for the red scrollbar that displays all three color values and the color sample.
+   - Attach the event handler to the green and blue scrollbars, as well as the red one.

> > **NOTE** You can download the code and resources for this lesson from the web-site at www.wrox.com/go/csharptwentyfour2e.

# ## Hints

This Try It requires a few techniques that haven’t been covered yet, but it’s not too hard to build with a couple of hints.

+   - A scrollbar’s value property is an integer. To convert it into a string so you can display it in a label, call its `ToString` method. For example, the following code makes the `redLabel` control display the `redHScrollBar`’s value property:
+   
+       ```csharp
+       redLabel.Text = redHScrollBar.Value.ToString();
+       ```
+   - The `color` class’s `FromArgb` method returns a color with given red, green, and blue color components between 0 and 255. For example, `Color.FromArgb(255, 128, 0)` returns the color orange (red = 255, green = 128, and blue = 0). Pass this method the values selected by the scrollbars (returned by their value properties) and assign the result to the sample label’s `BackColor` property.