
### 5 Get drawing

To draw your pet, add these instructions above the last two lines of code. There's a separate command for each body part. The numbers, called coordinates, tell Tkinter what to draw and where to draw it.

Storing the body colour in the variable c.body_color means you don't have to keep typing in 'SkyBlue1'.

```python
c.configure(bg='dark blue', highlightthickness=0)
c.body_color = 'SkyBlue1'

body = c.create_oval(35, 20, 365, 350, outline=c.body_color, fill=c.body_color)
ear_left = c.create_polygon(75, 80, 75, 10, 165, 70, outline=c.body_color, fill=c.body_color)
ear_right = c.create_polygon(255, 45, 325, 10, 320, 70, outline=c.body_color, \
                             fill=c.body_color)
foot_left = c.create_oval(65, 320, 145, 360, outline=c.body_color, fill=c.body_color)
foot_right = c.create_oval(250, 320, 330, 360, outline=c.body_color, fill=c.body_color)

eye_left = c.create_oval(130, 110, 160, 170, outline='black', fill='white')
pupil_left = c.create_oval(140, 145, 150, 155, outline='black', fill='black')
eye_right = c.create_oval(230, 110, 260, 170, outline='black', fill='white')
pupil_right = c.create_oval(240, 145, 250, 155, outline='black', fill='black')

mouth_normal = c.create_line(170, 250, 200, 272, 230, 250, smooth=1, width=2, state=NORMAL)

c.pack()
```

In the code, 'left' and 'right' refer to the left and right of the window as you look at it.

These pairs of coordinates define the start, mid-point, and end of the mouth.

The mouth is a smooth line, 2 pixels wide.

### Expert Tips

**Tkinter coordinates**

The drawing instructions use x and y coordinates. In Tkinter, the x coordinates start at 0 on the left and increase as you move across the window, until they reach 400 on the far right. The y coordinates start at 0 at the top. They get bigger as you move down, until they reach 400 at the bottom.

![](img/1bd24ab186f69fb18194b4174ca15178_144_0.png)

![](img/1bd24ab186f69fb18194b4174ca15178_144_1.png)

### 6 Run it again

Run the program again and you should see Screen Pet sitting in the middle of the Tkinter window.

## Blinking pet

Your Screen Pet looks cute, but it's not doing anything! Let's write some code to get it blinking. You'll need to create two functions: one to open and shut the eyes, the other to tell them how long to stay open and shut for.

![](img/1bd24ab186f69fb18194b4174ca15178_145_0.png)

To blink, the eyes fill with sky blue and the pupils disappear.

### 7 Open and close the eyes

Create this function, toggle_eyes(), at the top of your file, under the first line of code. It makes the eyes look closed by hiding the pupils and filling the eyes with the same colour as the body. It also switches the eyes between being open and closed.

First the code checks the eyes' current colour: white is open, blue is closed.

This line sets the eyes' new_color to the opposite value.

```python
from tkinter import HIDDEN, NORMAL, Tk, Canvas

def toggle_eyes():
    current_color = c.itemcget(eye_left, 'fill')
    new_color = c.body_color if current_color == 'white' else 'white'
    current_state = c.itemcget(pupil_left, 'state')
    new_state = NORMAL if current_state == HIDDEN else HIDDEN
    c.itemconfigure(pupil_left, state=new_state)
    c.itemconfigure(pupil_right, state=new_state)
    c.itemconfigure(eye_left, fill=new_color)
    c.itemconfigure(eye_right, fill=new_color)
```

Now the code checks if the current state of the pupils is NORMAL (visible) or HIDDEN (not visible).

These lines change the visibility of the pupils.

This line sets the pupils' new_state to the opposite value.

These lines change the eyes' fill colour.

### LINGO

**Toggling**

Switching between two states is known as "toggling". So you "toggle" the lights in your house when you switch them on and off. The blinking code switches, or toggles, between Screen Pet's eyes being open and closed. If the eyes are closed when you run it, they'll change to being open. If they're open, they'll change to being closed.

![](img/1bd24ab186f69fb18194b4174ca15178_145_1.png)

### 8 Realistic blinking

The eyes need to close only briefly and stay open for a while between blinks. Add this function, `blink()`, under the code you typed in Step 7. It blinks the eyes for a quarter of a second (250 milliseconds), then finishes with a command that tells `mainloop()` to call it again after 3 seconds (3,000 milliseconds).

```python
c.itemconfigure(eye_right, fill=new_color)

def blink():
    toggle_eyes()
    root.after(250, toggle_eyes)
    root.after(3000, blink)

root = Tk()
```

Close the eyes.

Wait 250 milliseconds, then open the eyes.

Wait 3,000 milliseconds, then blink again.

### 9 Animate!

Put this line in the main part of your program, just above the last line. Now run the program. Your pet will come to life after 1 second (1,000 milliseconds) and sit there blinking until you close the window.

```python
root.after(1000, blink)
root.mainloop()
```

Wait 1,000 milliseconds, then start blinking.

## Changing moods

Screen Pet looks quite happy just now, with its little smile, but let's cheer it up even more. We'll give it a bigger, beaming smile and bright, rosy cheeks.

![](img/1bd24ab186f69fb18194b4174ca15178_146_0.png)

### 10 Make a happy face

Add this code to the part of the program that draws Screen Pet, after the line that creates the "normal" mouth. As well as a happy mouth and pink cheeks, it also draws a sad mouth. They will all remain hidden for now.

Create a happy mouth.

Create a sad mouth.

```python
mouth_normal = c.create_line(170, 250, 200, 272, 230, 250, smooth=1, width=2, state=NORMAL)
mouth_happy = c.create_line(170, 250, 200, 282, 230, 250, smooth=1, width=2, state=HIDDEN)
mouth_sad = c.create_line(170, 250, 200, 232, 230, 250, smooth=1, width=2, state=HIDDEN)

cheek_left = c.create_oval(70, 180, 120, 230, outline='pink', fill='pink', state=HIDDEN)
cheek_right = c.create_oval(280, 180, 330, 230, outline='pink', fill='pink', state=HIDDEN)

c.pack()
```

These lines create pink, blushing cheeks.

### 11 Show the happy face

Next, create a function called `show_happy()` to reveal the happy expression when you move the mouse pointer over Screen Pet as if you were stroking it. Type this code beneath the `blink()` function you added in Step 8.

### LINGO

**Event handler**

The function `show_happy()` is an event handler. This means it's only called when a particular event happens, so that it can deal with it. In your code, stroking your pet calls `show_happy()`. In real life, you might call a “mop the floor” function to handle a “spill drink” event!

![](img/1bd24ab186f69fb18194b4174ca15178_147_0.png)

The if line checks to see if the mouse pointer is over the pet.

```python
root.after(3000, blink)

def show_happy(event):
    # event.x and event.y are the coordinates of the mouse-pointer.
    if (20 <= event.x <= 350) and (20 <= event.y <= 350):
        c.itemconfigure(cheek_left, state=NORMAL)   # Show the pink cheeks.
        c.itemconfigure(cheek_right, state=NORMAL)
        c.itemconfigure(mouth_happy, state=NORMAL)  # Show the happy mouth.
        c.itemconfigure(mouth_normal, state=HIDDEN) # Hide the normal mouth.
        c.itemconfigure(mouth_sad, state=HIDDEN)    # Hide the sad mouth.
    return
```

### Expert Tips

**Focus**

Tkinter won't be able to spot you moving the mouse-pointer over the window to stroke Screen Pet unless the window is “in focus”. You can get it in focus by clicking once anywhere in the window.

![](img/1bd24ab186f69fb18194b4174ca15178_147_1.png)

### 12 Happy moves

When the program starts, Screen Pet blinks without you doing anything. But to get it to look happy when it's being stroked, you need to tell it what event to look out for. Tkinter calls the mouse-pointer moving over its window a `<Motion>` event. You need to link this to the handler function by using Tkinter's `bind()` command. Add this line to the main part of your program. Then run the code and stroke the pet to try it out.

```python
c.pack()

c.bind('<Motion>', show_happy)  # This command links the moving mouse-pointer to the happy face.

root.after(1000, blink)
root.mainloop()
```
