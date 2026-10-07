The UseTextBox example program is similar to the UseRichTextBox program except it demonstrates the TextBox control instead of the RichTextBox control. Its menu let you change the properties of all the control's text, not just the selected text as program UseRichTextBox does. Because the TextBox doesn't support bulleted or numbered paragraphs, the UseTextBox program's Paragraph menu doesn't provide these commands.

Figure 7-17 shows the UseTextBox program in action. Notice how the font styles, colors, and alignment apply to the controls, not just parts of the text.

![](bbox=[0.586, 0.073, 0.951, 0.259])

FIGURE 7-17

# SUMMARY

This chapter describes WPF's most useful user interaction controls. These are the controls that allow the user to control and provide input to a program.

This chapter provides a brief overview of the controls and gives enough detail for you to get started using them. However, some of the controls are fairly complex. The RichTextBox control is remarkably complicated and provides a wide variety of formatting options and editing commands. You'll need to spend some time experimenting with the RichTextBox control before you can use its capabilities to its fullest.

This chapter and the previous two describe major categories of WPF controls. Chapter 5 describes content controls — controls that display output for the user to view. The following chapter provides more detail on a specific kind of control: those that produce two-dimensional shapes. These include Line, Ellipse, Rectangle, Polygon, Polyline, and Path. While many applications rely primarily on textual controls such as Labels and TextBoxes, these drawing controls can be very useful for visualizing data.