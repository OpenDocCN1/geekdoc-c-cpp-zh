You can set other behaviors with the `setFocusLostBehavior` method. The “commit” behavior is subtly different from the default. If the text string is invalid, then both the text string and the field value stay unchanged—they are now out of sync. The “persist” behavior is even more conservative. Even if the text string is valid, neither the text field nor the current value are changed. You would need to call `commitEdit`, `setValue`, or `setText` to bring them back in sync. Finally, there is a “revert” behavior that doesn’t seem to be useful at all: Whenever focus is lost, the user input is disregarded, and the text string reverts to the old value.

> **NOTE:** Generally, the “commit or revert” default behavior is reasonable. There is just one potential problem. Suppose a dialog box contains a text field for an integer value. A user enters a string "1729", with a leading space, and clicks the OK button. The leading space makes the number invalid, and the field value reverts to the old value. The action listener of the OK button retrieves the field value and closes the dialog box. The user never knows that the new value has been rejected. In this situation, it is appropriate to select the “commit” behavior and have the OK button listener check that all field edits are valid before closing the dialog box.

# 10.4.2.3 Filters

The basic functionality of formatted text fields is straightforward and sufficient for most uses. However, you can add a couple of refinements. Perhaps you want to prevent the user from entering nondigits altogether. You can achieve that behavior with a *document filter*. Recall that in the model-view-controller architecture, the controller translates input events into commands that modify the underlying document of the text field—that is, the text string stored in a `PlainDocument` object. For example, whenever the controller processes a command that causes text to be inserted into the document, it calls the “insert string” command. The string to be inserted can be either a single character or the content of the paste buffer. A document filter can intercept this command and modify the string or cancel the insertion altogether. Here is the code for the `insertString` method of a filter that analyzes the string to be inserted and inserts only the characters that are digits or a minus sign. (The code handles supplementary Unicode characters, as explained in Volume I, Chapter 3. See Chapter 2 for the `StringBuilder` class.)

```
public void insertString(FilterBypass fb, int offset, String string, AttributeSet attr)
    throws BadLocationException
{
    StringBuilder builder = new StringBuilder(string);
    for (int i = builder.length() - 1; i >= 0; i--)
    {
        int cp = builder.codePointAt(i);
```