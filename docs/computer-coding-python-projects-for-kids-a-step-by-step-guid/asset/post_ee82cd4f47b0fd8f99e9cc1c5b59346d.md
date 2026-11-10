
**REMEMBER**

## Nested loops

You might remember reading about nested loops on page 35. You can put as many loops inside one another as you want. In this project, the outer loop runs six times. Each time the outer loop runs, the inner loop runs four times. So in total, the inner loop runs 6 × 4 = 24 times.

![](img/1bd24ab186f69fb18194b4174ca15178_184_0.png)

- 9. **Start the main loop**

  Now start Tkinter's mainloop. Once this loop starts, the GUI will be displayed and it will start listening for button presses. Type this line after the code you added in Step 8.

```python
button_symbols[x, y] = symbols.pop()

root.mainloop()
```

- 10. **Test your code**

  Run the program again. Your Tkinter window should now be filled with 24 buttons arranged in a grid. If it doesn't look similar to the picture shown here, check your code carefully for any errors.

![](img/1bd24ab186f69fb18194b4174ca15178_184_1.png)

![](img/1bd24ab186f69fb18194b4174ca15178_184_2.png)

## Show the symbol

Finally, you need to create the function that handles the button presses. This function will always display a symbol, but how it operates depends on whether it’s the first or second turn in the matching attempt. If it’s the first turn, the function just needs to remember which button was pressed. If it’s the second turn, it needs to check if the symbols match. Symbols that don’t match are hidden. Matching symbols are left showing and their buttons are disabled.

```python
from tkinter import Tk, Button, DISABLED

def show_symbol(x, y):
    global first
    global previousX, previousY
    buttons[x, y]['text'] = button_symbols[x, y]
    buttons[x, y].update_idletasks()

    if first:
        previousX = x
        previousY = y
        first = False
    elif previousX != x or previousY != y:
        if buttons[previousX, previousY]['text'] != buttons[x, y]['text']:
            time.sleep(0.5)
            buttons[previousX, previousY]['text'] = ''
            buttons[x, y]['text'] = ''
        else:
            buttons[previousX, previousY]['state'] = DISABLED
            buttons[x, y]['state'] = DISABLED
        first = True
```

The x and y values tell the function which button has been pressed.

These lines tell the program that the variables are global.

These lines show the symbol.

If it’s the first turn, the code remembers the button press by storing the x and y coordinates.

Second turn. This line includes a check to stop the player cheating by pressing the same button twice!

If the symbols don’t match...

If the symbols match...

Wait 0.5 seconds to give the player time to see the symbols, then hide them.

Disable the pair of matching buttons so the player can’t press them again.

This line gets the function ready for the first button press of the next attempt.

### How it works

The function shows a button’s symbol by changing its text label to the Unicode character we randomly assigned to it. We use `update_idletasks()` to tell Tkinter to show this symbol right now. If it’s the first turn, we just store the button’s coordinates in variables. If it’s the second turn, we need to check the player isn’t trying to cheat by hitting the same button twice. If they aren’t, we check if the symbols match. If the symbols don’t match, we hide them by setting the text to empty strings; if they do match, we leave them showing but disable the buttons.

![](img/1bd24ab186f69fb18194b4174ca15178_185_0.png)

> We take matching very seriously!

## Hacks and tweaks

You could adapt this game in many ways. You can show the number of moves taken to finish the game, so the player can try and beat their own score or challenge their friends. You could also add more symbols to make the game harder.

### Show the number of moves

At the moment, the player has no way of knowing how well they’ve done or if they’ve done any better than their friends. How can we make the game more competitive? Let’s add a variable to count how many turns a player takes to finish the game. Then players can compete to see who gets the lowest score.

![](img/1bd24ab186f69fb18194b4174ca15178_186_0.png)

- 1. **Add a new module**

  You need to import Tkinter’s messagebox widget to display the number of moves at the end of the game. In the import line, add the word `messagebox` after `DISABLED`.

```python
from tkinter import Tk, Button, DISABLED, messagebox
```

- 2. **Make new variables**

  You’ll have to make two extra variables for this hack. One variable will keep track of the number of moves the player makes, while the other will remember how many pairs they’ve found. Give them both a starting value of 0. Put these lines below the variable `previousY`.

```python
previousY = 0
moves = 0
pairs = 0
```

The player hasn’t made any moves yet, or found any pairs, so the values are 0.

- 3. **Declare them global**

  The moves and pairs variables are global variables, and they’ll need to be changed by the `show_symbol()` function. Let `show_symbol()` know this by putting these two lines near the top of the function.

```python
def show_symbol(x, y):
    global first
    global previousX, previousY
    global moves
    global pairs
```

- 4. **Count the moves**

  A move is two button presses (one matching attempt). So you only need to add 1 to the `moves` variable when the `show_symbol()` function is called for the first or the second button press—not for both. Let’s do it for the first button press. Change the `show_symbol()` function to look like this.

```python
if first:
    previousX = x
    previousY = y
    first = False
    moves = moves + 1
```

- 5. **Display a message**

  Now add the following code near the bottom of the `show_symbol()` function. It will track the matched pairs and show a message box at the end of the game telling the player how many moves they took. When the player clicks the box’s OK button, the code calls the `close_window()` function, which we’ll add next.

![](img/1bd24ab186f69fb18194b4174ca15178_187_0.png)

```python
buttons[x, y]['state'] = DISABLED
pairs = pairs + 1
if pairs == len(buttons)/2:
    messagebox.showinfo('Matching', 'Number of moves: ' +
                        str(moves), command=close_window)
```

Add 1 to the number of pairs found.

This line displays a box showing the number of moves.

If all the pairs have been found, run the code under this line.

**How it works**

There are 12 pairs of symbols, so you could simply have typed `pairs == 12` in the hack. However, your code is smarter than this. It calculates the number of pairs by using `pairs == len(buttons)/2`. This allows you to add more buttons to the game without having to update this bit of code.

- 6. **Close the window**

  Finally, you need to create a `close_window()` function, to make the program exit the game when the player clicks the OK button on the “Number of moves” message box. Add this code under the line that imports the modules.

```python
def close_window(self):
    root.destroy()
```

This command closes the window.

### Add more buttons

Let's really challenge the player's memory by adding more buttons and symbols to the game.

![](img/1bd24ab186f69fb18194b4174ca15178_188_0.png)

I think it could do with a few more buttons!

**1 Extra symbols**

First you need to add more pairs to the symbols list. Include this new line in the code.

| 符号 | Unicode | 符号 | Unicode | 符号 | Unicode |
|---|---|---|---|---|---|
| ✳ | U+2733 | ✴ | U+2734 | ❄ | U+2744 |

```python
symbols = [u'\u2702', u'\u2702', u'\u2705', u'\u2705', u'\u2708', u'\u2708',
           u'\u2709', u'\u2709', u'\u270A', u'\u270A', u'\u270B', u'\u270B',
           u'\u270C', u'\u270C', u'\u270F', u'\u270F', u'\u2712', u'\u2712',
           u'\u2714', u'\u2714', u'\u2716', u'\u2716', u'\u2728', u'\u2728',
           u'\u2733', u'\u2733', u'\u2734', u'\u2734', u'\u2744', u'\u2744']
```

Add the three pairs of new symbols to the end of the list.

**2 Extra buttons**

Now add an extra row of buttons.
To do this, you just need to change the y range in the nested loops from 4 to 5, as shown on the right.

```python
for x in range(6):
    for y in range(5):
```

This line will now create five rows of buttons instead of four.

**3 Even bigger?**

You now have a total of 30 buttons. If you want to add more, make sure that the number of extra buttons you add is a multiple of 6 so that you always add complete rows. If you're feeling adventurous, you could experiment with different button layouts by changing the nested loops.

| 符号 | Unicode | 符号 | Unicode | 符号 | Unicode | 符号 | Unicode | 符号 | Unicode |
|---|---|---|---|---|---|---|---|---|---|
| ❇ | U+2747 | ❌ | U+274C | ❎ | U+274E | ❓ | U+2753 | ❔ | U+2754 |
| ❕ | U+2755 | ❗ | U+2757 | ❤ | U+2764 | ➕ | U+2795 | ➖ | U+2796 |
| ➗ | U+2797 | ➡ | U+27A1 | ➰ | U+27B0 |  |  |  |  |
