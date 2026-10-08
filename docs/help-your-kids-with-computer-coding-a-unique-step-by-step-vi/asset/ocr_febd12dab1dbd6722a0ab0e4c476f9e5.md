# # Reacting to events

Computers receive a signal when a key is pressed or a mouse is moved. This is called an “event”. Programs can instruct the computer to respond to any events it detects.

+   SEE ALSO
* 158–159 Making shapes
* 160–161 Changing things

# Event names

Lots of different events can be triggered using input devices like a mouse or keyboard. Tkinter has names to describe each of these events.

![](bbox=[0.535, 0.259, 0.934, 0.335])

# Mouse events

# Keyboard events

![](bbox=[0.066, 0.42, 0.934, 0.6])

To make a program respond to mouse events, simply link (or bind) a function to an event. Here, the function “burp” is created, then bound to the “Button-1” event.

This brings the Tkinter window to the front of your screen

![](bbox=[0.535, 0.67, 0.934, 0.955])

```
window.attributes('-topmost', 1)
def burp(event):
    mouth_open()
    c.itemconfig(words, text='Burp!')
c.bind_all('<Button-1>', burp)
```