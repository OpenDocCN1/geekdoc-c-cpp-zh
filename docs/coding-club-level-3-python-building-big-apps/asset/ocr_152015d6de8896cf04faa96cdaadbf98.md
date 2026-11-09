# # Getting the bats to move

If you run `main.py` now, you will find that the bats do not appear.

# ## Quick Quiz 5.1

+   **Why do the bats not appear?**
+   
+   A. We have not ordered any bats in `main.py`.
+   B. We have not attached their methods to any keyboard input.
+   C. We have not typed out the code correctly.
+   D. Table does not know how to draw bats.

So we need to send some orders from `main.py` to our new bat factory for a left and right bat. You should now copy the new code from Code Box 5.2 into `main.py`.

First we order two bats from our new class. Then we attach the movement methods to key presses on the keyboard – you will remember from Python Basics that this is pleasingly simple in Python. Here again there is a start file where you will find some spaces for you to add the new code.

```
### Code Box 5.2 — `main.py`

```python
from tkinter import *
import table, ball, bat

# initialise global variables
x_velocity = 10
y_velocity = 10
```

_Do not forget to import the bat class!_
```