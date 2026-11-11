# 11.3.3 Password Fields

Password fields are a special kind of text fields. To prevent nosy bystanders from seeing your password, the characters that the user enters are not actually displayed. Instead, each typed character is represented by an *echo character*, such as a bullet (•). Swing supplies a `JPasswordField` class that implements such a text field.

The password field is another example of the power of the model-view-controller architecture pattern. The password field uses the same model to store the data as a regular text field, but its view has been changed to display all characters as echo characters.

| `javax.swing.JPasswordField` | `1.2` |
|---|---|
| • `JPasswordField(String text, int columns)` | constructs a new password field. |
| • `void setEchoChar(char echo)` | sets the echo character for this password field. This is advisory; a particular look-and-feel may insist on its own choice of echo character. A value of `0` resets the echo character to the default. |
| • `char[] getPassword()` | returns the text contained in this password field. For stronger security, you should overwrite the content of the returned array after use. (The password is not returned as a `String` because a string would stay in the virtual machine until it is garbage-collected.) |

# 11.3.4 Text Areas

Sometimes, you need to collect user input that is more than one line long. As mentioned earlier, you can use the `JTextArea` component for this. When you place a text area component in your program, a user can enter any number of lines of text, using the Enter key to separate them. Each line ends with a `\n`. Figure 11.11 shows a text area at work.

In the constructor for the `JTextArea` component, specify the number of rows and columns for the text area. For example,

```
textArea = new JTextArea(8, 40); // 8 lines of 40 columns each
```

where the columns parameter was as before—and you still need to add a few more columns for safety’s sake. Also, as before, the user is not restricted to the number of rows and columns; the text simply scrolls when the user inputs