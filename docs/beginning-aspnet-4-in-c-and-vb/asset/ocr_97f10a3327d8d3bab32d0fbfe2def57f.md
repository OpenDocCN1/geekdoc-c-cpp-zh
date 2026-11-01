![](bbox=[0.11, 0.14, 0.59, 0.48])

# FIGURE 48-17

The File menu has two options: Open, which evokes OpenFileDialog when selected and reads in whatever file the user clicks, and Exit, which closes the application when clicked. Figure 48-18 shows CapsEditor displaying its own source file, Form1.cs. (A few lines have been double-clicked in this image to convert them to uppercase.)

![](bbox=[0.12, 0.61, 0.6, 0.83])

# FIGURE 48-18

The sizes of the horizontal and vertical scrollbars are correct. The client area will scroll just enough to view the entire document. CapsEditor does not try to wrap lines of text — the example is already complicated enough as it is. It just displays each line of the file exactly as it is read in. There are no limits to the size of the file, but you are assuming that it is a text file and does not contain any nonprintable characters.

Begin by adding a using command:

```
using System;
using System.Collections;
using System.ComponentModel;
```