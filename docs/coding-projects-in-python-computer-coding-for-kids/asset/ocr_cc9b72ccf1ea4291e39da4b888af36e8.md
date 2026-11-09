```
```python
arc = c.create_arc(235, 120, 365, 370, outline='black', \
    fill='black', state=HIDDEN)
```
```

![](bbox=[0.695, 0.081, 0.844, 0.132])

```
```python
arc = c.create_arc(235, 120, 365, 370, outline='red', \
    fill='red', state=HIDDEN, style=CHORD)
```
```

![](bbox=[0.696, 0.177, 0.847, 0.228])

```
```python
arc = c.create_arc(235, 120, 365, 370, outline='green', \
    fill='green', state=HIDDEN, style=ARC)
```
```

![](bbox=[0.695, 0.272, 0.844, 0.331])

# Draw lines

Now try adding some lines to our list of shapes using the create_line() function.

```
```python
line = c.create_line(35, 200, 365, 200, fill='blue', state=HIDDEN)
```
```

![](bbox=[0.816, 0.452, 0.979, 0.464])

```
```python
line = c.create_line(35, 20, 365, 350, fill='black', state=HIDDEN)
```
```

![](bbox=[0.818, 0.494, 0.983, 0.579])

# Draw polygons

Next try making some polygons for your shape collection, using create_polygon(). You’ll need to give coordinates for each corner of your polygon.

The three pairs of numbers in the code give the coordinates of the three corners of the triangle.

```
```python
polygon = c.create_polygon(35, 200, 365, 200, 200, 35,
outline='blue', fill='blue', state=HIDDEN)
```
```

![](bbox=[0.819, 0.675, 0.978, 0.744])

# Stop players cheating

Right now, if a shape is called and both players hit the shape key at the same time, they each get a point. In fact, they will still be able to score points up until the next shape is shown, since the previous and current will still be the same. Try this hack to stop the players from cheating.

# Go global

Now we need to set the previous_color and current_color variables on the snap() function because these are not accessible from inside the function unless we make them global variables.

```
```python
global previous_color
```
```