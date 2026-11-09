To understand the coordinates, it helps to know that unlike in maths and science at school, computers often count pixels from the top left corner of the screen or window. This is the case in Python. Look at Figure 3.3 to see how this works.

![](bbox=[0.053, 0.229, 0.491, 0.667])

**Figure 3.3** Coordinates.

So the call to implement the `create_line()` method, could be written as:

```
```python
self.canvas.create_line(300, 0, 300, 400, width=2, fill=net_colour, dash=(15, 23))
```
```