# 13. Hide the happy face

You only want Screen Pet to look really happy when you're actually stroking it. Add a new function, `hide_happy()`, below the code for `show_happy()`. (This new code will set Screen Pet's expression back to normal.)

```
```python
def hide_happy(event):
    c.itemconfigure(cheek_left, state=HIDDEN)
    c.itemconfigure(cheek_right, state=HIDDEN)
    c.itemconfigure(mouth_happy, state=HIDDEN)
    c.itemconfigure(mouth_normal, state=NORMAL)
    c.itemconfigure(mouth_sad, state=HIDDEN)
    return
```
```

Hide the pink cheeks.

Hide the happy mouth.

Show the normal mouth.

Hide the sad mouth.

![](bbox=[0.808, 0.069, 0.946, 0.192])

Don't forget to save your work.

# 14. Call the function

Type this line to call `hide_happy()` when the mouse pointer leaves the window. It links Tkinter's `<Leave>` event to `hide_happy()`. Now test your code.

```
```python
c.bind('<Motion>', show_happy)
c.bind('<Leave>', hide_happy)

root.after(1000, blink)
```
```

# What cheek!

So far, your pet has been very well behaved. Let's give it a cheeky personality! You can add some code that will make Screen Pet stick its tongue out and cross its eyes when you tickle it by double-clicking on it.

![](bbox=[0.616, 0.557, 0.892, 0.788])

# 15. Draw the tongue

Add these lines to the code that draws Screen Pet, under the line that creates the sad mouth. The program will draw the tongue in two parts, a rectangle and an oval.

```
```python
mouth_sad = c.create_line(170, 250, 200, 232, 230, 250, smooth=1, width=2, state=HIDDEN)
tongue_main = c.create_rectangle(170, 250, 230, 290, outline='red', fill='red', state=HIDDEN)
tongue_tip = c.create_oval(170, 285, 230, 300, outline='red', fill='red', state=HIDDEN)

cheek_left = c.create_oval(70, 180, 120, 230, outline='pink', fill='pink', state=HIDDEN)
```
```