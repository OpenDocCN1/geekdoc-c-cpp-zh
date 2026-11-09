You can now add the extra code in Code Box 3.2 to your copy of `table.py`. Use the comments in the supplied file to guide you as to where to add the new code.

# Code Box 3.2

```
```python
# order a canvas to draw on from the tkinter factory:
self.canvas = Canvas(window, bg=self.colour, height=self.height, width=self.width)
self.canvas.pack()

# add a net to the canvas using a method from the tkinter factory:
if(vertical_net):
    self.canvas.create_line(self.width/2, 0, self.width/2,
                            self.height, width=2, fill=net_colour, dash=(15, 23))
if(horizontal_net):
    self.canvas.create_line(0, self.height/2, self.width,
                            self.height/2, width=2, fill=net_colour, dash=(15, 23))
```
```

# Warning!

It is easy to make a typing mistake at some stage. Check your code carefully and when you complete it, run the program and see if you can find and correct any problems. If you have any difficulties and start to get frustrated, then the complete file is available from the companion website. After all, coding should be fun. Before using the complete files, please do try to type the code in yourself and think about how each line of code works as you type. You will learn to code better if you do this. (This phrase appears to be in an infinite loop!)