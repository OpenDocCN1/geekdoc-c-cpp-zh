# 10.4 Text Components

Figure 10.35 shows all text components that are included in the Swing library. You already saw the three most commonly used components—`JTextField`, `JPasswordField`, and `JTextArea`—in Volume I, Chapter 9. In the following sections, we will introduce the remaining text components. We will also discuss the `JSpinner` component that contains a formatted text field together with tiny “up” and “down” buttons to change its contents.

![](bbox=[0.12, 0.32, 0.79, 0.62])

**Figure 10.35** The hierarchy of text components and documents

All text components render and edit the data stored in a model object of a class implementing the `Document` interface. The `JTextField` and `JTextArea` components use a `PlainDocument` that simply stores a sequence of lines of plain text without any formatting.

A `JEditorPane` can show and edit styled text (with fonts, colors, etc.) in a variety of formats, most notably HTML; see Section 10.4.4, “Displaying HTML with the `JEditorPane`” on p. 712. The `StyledDocument` interface describes the additional requirements of styles, fonts, and colors. The `HTMLDocument` class implements this interface.

The subclass `JTextPane` of `JEditorPane` also holds styled text as well as embedded Swing components. We do not cover the very complex `JTextPane` in this book but instead