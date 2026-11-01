| PROPERTY | DESCRIPTION |
|---|---|
| `Stretch` | It's actually pretty rare to have an image that is exactly the right size for your purpose, and sometimes the size of the image must change as the application window is resized. You can use this property to control how the image behaves. There are four possibilities:

None — The image doesn't resize.
Fill — The image resizes to fill the entire space. This may contort the image.
Uniform — The image keeps its aspect ratio and doesn't fill the available space if this would change the aspect ratio.
UniformToFill — The image keeps its aspect ratio and fills the available space. If keeping the ratio means that some of the image is too large for the space available, the image is clipped to fit. |

# The Label Control

You have already seen this most simple of controls used in some of the previous examples. It displays simple text information to the user and in some cases relays information about shortcut keys. The control uses the `Content` property to display its text. The `Label` control displays text on a single line. If you prefix a letter with an underscore “ _ ” character, the letter will become underlined and it will then be possible to access the control directly by using the prefixed letter and Alt. For example, `_Name` assigns the shortcut Alt+N to any control directly following the label.

# The TextBlock Control

Like `Label`, this control displays simple text without any complicated formatting. Unlike the `Label`, the `TextBlock` control is capable of displaying multiple lines of text. It is not possible to format individual parts of the text.

The `TextBlock` displays the text even if it will not fit in the space granted to the control. The control itself does not provide any scrollbars in this case, but it can be wrapped in a handy view control when needed: the `ScrollViewer`.

# The Button Control

Like the `Label` control, you have already seen quite a bit of the `Button` control. This control is used everywhere and is easily recognized on a user interface. Your users will expect that they can left-click it to perform an action — no more and no less. Altering this behavior will most likely lead to bad interface design and frustrated users.

By default, the button displays itself with a single short line of text or an image that describes what happens when you click on it.

The button does not contain any properties to display images or text, but you can use the `Content` property to display simple text or embed an `Image` control in the content to display an image. You can find this code in the downloaded code at Ch14Ex01\ImageButton.xaml: