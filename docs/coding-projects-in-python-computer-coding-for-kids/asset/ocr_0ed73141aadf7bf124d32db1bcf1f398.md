# 11  **Draw the eyes**

Let’s add some eyes so that the robot can see where it’s going. To do this, you’ll draw a large white rectangle with two smaller squares inside it (for pupils). You don’t have to write a new function to draw squares, since a square is a rectangle with all its sides the same length. Insert these commands under the code you added in Step 10.

```
```python
# eyes
t.goto(-60, 160)
rectangle(30, 10, 'white')
t.goto(-55, 155)
rectangle(5, 5, 'black')
t.goto(-40, 155)
rectangle(5, 5, 'black')
```
```

Draw the white part of the eyes.

Draw the left pupil.

Draw the right pupil.

> > I’ve got eyes, but I still keep walking into things!!

![](bbox=[0.063, 0.263, 0.874, 0.494])

# 12  **Draw the mouth**

Now give the robot a mouth. Type these commands under the code you added in Step 11.

```
```python
# mouth
t.goto(-65, 135)
rectangle(40, 5, 'black')
```
```

# 13  **Hide the turtle**

Finally, hide the turtle so it doesn’t look odd sitting on the robot’s face. Type this line after the code you added in Step 12. Run the program to see the whole robot being built.

```
```python
t.hideturtle()
```
```

This makes the turtle invisible.

> > I need a vacation!

> > I love to watch these robots being built!

![](bbox=[0.056, 0.731, 0.991, 0.968])