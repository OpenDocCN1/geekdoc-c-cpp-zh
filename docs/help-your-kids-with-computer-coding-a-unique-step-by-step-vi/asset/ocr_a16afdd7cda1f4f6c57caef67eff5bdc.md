# Hide and show

Shapes can be hidden using the "itemconfig() function. If you hide the eyeball, and then show it again a moment later, the alien looks as though it is blinking.

Blinking alien
To make the alien blink, you need to hide the pupil and make the white of the alien green.

![](bbox=[0.588, 0.083, 0.715, 0.203])

+   Create blinking functions
This code creates two functions so you can make the alien blink.

Blink and unblink
Type this code into the shell window to make the alien blink.

Turns the white of the alien green

```
def blink():
  itemconfig(eye, fill='green')
  itemconfig(eyeball, state=HIDDEN)
def unblink():
  white again
  itemconfig(eye, fill='white')
  itemconfig(eyeball, state=NORMAL)
```

```
>>> blink()
>>> unblink()
```

The shape's ID

"unblink()"
command makes the eye appear open again

Hides the pupil

Reveals the pupil

# Saying things

Text can also be displayed on the screen to make the alien talk. You can even make it say different things in response to user commands.

> I am an alien!

+   Adding text
This code adds text to the graphic of the alien and creates a function to steal its hat.

Positions the text
on the canvas

Put what you want
the alien to say in
quote marks

```
words = c.create_text(200, 280, text='I am an alien!')
def steal_hat():
  itemconfig(hat, state=HIDDEN)
  itemconfig(words, text='Give my hat back!')
```

Hides the
hat

As soon as the hat
disappears the alien
will ask for it

A new message
appears when the
hat

+   Steal the hat
Type this code into the shell window
and see what happens.

Type this to
steal the hat

```
>>> steal_hat()
```

Give my hat back!