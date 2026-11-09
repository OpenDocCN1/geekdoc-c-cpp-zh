# Get drawing

To draw your pet, add these instructions above the last two lines of code. There's a separate command for each body part. The numbers, called coordinates, tell Tkinter where to draw and where to draw it.

Storing the body color in the variable c.body_color means you don't have to keep typing in 'SkyBlue'.

```
```python
c.configure(bg='dark blue', highlightthickness=0)
c.body_color = 'SkyBlue'

body = c.create_oval(35, 20, 365, 350, outline=c.body_color, fill=c.body_color)
ear_left = c.create_polygon(75, 80, 75, 165, 10, 70, outline=c.body_color, fill=c.body_color)
ear_right = c.create_polygon(255, 85, 255, 165, 320, 70, outline=c.body_color, fill=c.body_color)

foot_left = c.create_oval(65, 320, 145, 360, outline=c.body_color, fill=c.body_color)
foot_right = c.create_oval(250, 320, 330, 360, outline=c.body_color, fill=c.body_color)

eye_left = c.create_oval(130, 110, 160, 170, outline='black', fill='white')
pupil_left = c.create_oval(140, 145, 150, 155, outline='black', fill='black')
eye_right = c.create_oval(230, 110, 260, 170, outline='black', fill='white')
pupil_right = c.create_oval(240, 145, 250, 155, outline='black', fill='black')

mouth_normal = c.create_line(170, 250, 200, 272, 230, 250, smooth=1, width=2, state=NORMAL)

c.pack()
```
```

In the code, “left” and “right” refer to the left and right of the window as you look at it.

These pairs of coordinates define the start, mid-point, and end of the mouth.

The mouth is a smooth line, 2 pixels wide.

# EXPERT TIPS

# Tinker coordinates

The drawing instructions use x and y coordinates. In Tkinter, the x coordinates start at 0 on the left and increase as you move across the window, until they reach 400 on the far right. The y coordinates also start at 0 on the left. They get bigger as you move down, until they reach 400 at the bottom.

Coordinates are written as pairs, with the x coordinate first.

![](bbox=[0.301, 0.756, 0.561, 0.919])

![](bbox=[0.641, 0.638, 0.914, 0.863])

# Run it again

Run the program again and you should see Screen Pet sitting in the middle of the Tkinter window.