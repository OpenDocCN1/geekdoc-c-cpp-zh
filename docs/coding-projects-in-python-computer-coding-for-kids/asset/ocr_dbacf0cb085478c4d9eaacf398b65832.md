# Getting started

In the first part of the project, you'll set up the graphical user interface (GUI) and add the pairs of symbols that will be hidden by the buttons.

+   1. **Create a new file**
+   
+   Open IDLE. Create a new file and save it as “matchmaker.py”.

![](bbox=[0.4, 0.23, 0.677, 0.332])

+   2. **Add modules**
+   
+   Now type this code at the top of your file to import the modules you need for this project. You’ll use `random` to shuffle the symbols, `time` to pause the program, and `Tkinter` to create the GUI.

```
```python
import random
import time
from tkinter import Tk, Button, DISABLED
```
```

`DISABLED` stops a button from responding after its symbol has been matched.

`Button` creates the buttons in the Tkinter window.

+   3. **Set up the GUI**
+   
+   Under the import commands, add this code, which will set up the GUI. The `root.resizable()` function prevents the player from resizing the window. This is important, since changing the size of the window will mess up the button layout that you’ll create later on.

```
```python
root = Tk()
root.title('Matchmaker')
root.resizable(width=False, height=False)
```
```

These lines create a Tkinter window and give it a title.

This line keeps the window at its original size.

+   4. **Test your code**
+   
+   Now run the code. You should see an empty Tkinter window with the heading “Matchmaker”. If you can’t see it, it’s probably hidden behind other windows.

![](bbox=[0.399, 0.733, 0.733, 0.967])

![](bbox=[0.531, 0.072, 0.972, 0.256])

Don't forget to save your work.