# ## Show the symbol

Finally, you need to create the function that handles the button presses. This function will always display a symbol, but how it operates depends on whether it’s the first or second turn in the matching attempt. If it’s the first turn, the function just needs to remember which button was pressed. If it’s the second turn, it needs to check if the symbols match. Symbols that don’t match are hidden. Matching symbols are left showing and their buttons are disabled.

```
~~~python
from tkinter import Tk, Button, DISABLED

# The x and y values tell the function which button has been pressed.
def show_symbol(x, y):
    # These lines tell the program that the variables are global
    global first
    global previousX, previousY
    # These lines show the symbol.
    buttons[x, y]['text'] = button_symbols[x, y]
    buttons[x, y].update_idletasks()

    if first:
        # If it's the first turn, the code remembers the button press by storing
        # the x and y coordinates.
        previousX = x
        previousY = y
        first = False
    # Second turn. This line includes a check to stop the player cheating by
    # pressing every button twice!
    elif previousX != x or previousY != y:
        # If the symbols don't match...
        if buttons[previousX, previousY]['text'] != buttons[x, y]['text']:
            # Wait 0.5 seconds to give the player time to see the symbols,
            # then hide them.
            time.sleep(0.5)
            buttons[previousX, previousY]['text'] = ''
            buttons[x, y]['text'] = ''
        else:
            # If the symbols match...
            # Disable the pair of matching buttons so the player can't press them again.
            buttons[previousX, previousY]['command'] = DISABLED
            buttons[x, y]['command'] = DISABLED
            # This line gets the function ready for the first button press of the next attempt.
            first = True
~~~
```

# ## How it works

The function shows a button’s symbol by changing its text label to the Unicode character we randomly assigned to it. We use update_idletasks() to tell Tkinter to show this symbol right now. If it’s the first turn, we just store the button’s coordinates in variables. If it’s the second turn, we need to check that the player isn’t trying to cheat by hitting the same button twice. If they aren’t, we check if the symbols match. If the symbols don’t match, we hide them by setting the text to empty strings; if they do match, we leave them showing but disable the buttons.

![](bbox=[0.7, 0.77, 0.96, 0.96])