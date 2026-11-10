# ### 8 Add some rectangles

Now create four different-coloured rectangles using Canvas's `create_rectangle()` function. Insert this block of code between the circle-drawing code and `c.pack()`. To avoid typing it all out, just type the first two lines, then copy and paste them three times and change the colours.

```
~~~python
shapes.append(circle)

rectangle = c.create_rectangle(35, 100, 365, 270, outline='black', fill='black', state=HIDDEN)
shapes.append(rectangle)
rectangle = c.create_rectangle(35, 100, 365, 270, outline='red', fill='red', state=HIDDEN)
shapes.append(rectangle)
rectangle = c.create_rectangle(35, 100, 365, 270, outline='green', fill='green', state=HIDDEN)
shapes.append(rectangle)
rectangle = c.create_rectangle(35, 100, 365, 270, outline='blue', fill='blue', state=HIDDEN)
shapes.append(rectangle)
c.pack()
~~~
```

![](bbox=[0.78, 0.09, 0.92, 0.21])

# ### 9 Add some squares

Next draw the squares. You can use the same function that you used to create the rectangles, but this time you'll turn the rectangles into squares by making all their sides the same length. Add this block of code between the rectangle code and `c.pack()`.

![](bbox=[0.58, 0.55, 0.95, 0.68])

```
~~~python
shapes.append(rectangle)

square = c.create_rectangle(35, 20, 365, 350, outline='black', fill='black', state=HIDDEN)
shapes.append(square)
square = c.create_rectangle(35, 20, 365, 350, outline='red', fill='red', state=HIDDEN)
shapes.append(square)
square = c.create_rectangle(35, 20, 365, 350, outline='green', fill='green', state=HIDDEN)
shapes.append(square)
square = c.create_rectangle(35, 20, 365, 350, outline='blue', fill='blue', state=HIDDEN)
shapes.append(square)
c.pack()
~~~
```