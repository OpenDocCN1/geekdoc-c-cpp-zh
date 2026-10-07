(continued)

| CONTROL | PURPOSE |
| :--- | :--- |
| ComboBox | Lets the user pick from a dropdown list of choices. |
| ContextMenu | Displays a pop-up menu associated with a control. |
| Frame | Displays Web or XAML content and provides simple navigation buttons. |
| GridSplitter | Lets the user resize the rows and columns in a Grid. |
| ListBox | Displays a list of items to the user and lets the user pick one or more, depending on how the control is configured. |
| Menu | Displays a main menu for a window. |
| PasswordBox | Lets the user enter text while hiding the text on the screen |
| RadioButton | Lets the user select one of an exclusive set of options. |
| RepeatButton | Lets the user fire Click repeatedly as long as the mouse is pressed over the control. |
| RichTextBox | Lets the user enter formatted text with such features as multiple fonts, multiple columns, paragraphs, indentation, bullets, and sort. |
| ScrollBar | Lets the user select a numeric value from a range of values. Usually the value is used to adjust something graphically such as the position of a large image within a viewing area. |
| Slider | Lets the user select a numeric value from a range of values. |
| TextBox | Lets the user enter text without fancy formatting. |

# BUTTON

The Button control lets the user click to tell the program to do something.

This is an extremely simple control to use. When the user clicks a Button, the Button raises its Click event. The program catches the event and whatever action is necessary.

The following code shows one of the simplest ways to attach an event handler to a Button in XAML code. When the user clicks on this button, the code-behind executes the routine named btnShowTime_Click:

```
<Button Content="Show Time" x:Name="btnShowTime" Width="100" Height="30" Margin="5" Click="btnShowTime_Click" />
```