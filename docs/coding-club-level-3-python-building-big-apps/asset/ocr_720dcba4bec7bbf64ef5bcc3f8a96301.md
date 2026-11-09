The method can be sent arguments to turn on and off this functionality for either vertical bats or horizontal bats. The new code can be seen in Code Box 5.6 but if you have downloaded the source code there is no need to copy it – it is supplied for your use.

# Code Box 5.6

```
```python
### methods
def detect_collision(self, ball, sides_sweet_spot=True, topnottom_sweet_spot=False):
    collision_direction = ""
    collision = False
    feel = 5
    # bat variables:
    top = self.y_posn
    bottom = self.y_posn + self.height
    left = self.x_posn
    right = self.x_posn + self.width
    v_centre = top + (self.height/2)
    h_centre = left + (self.width/2)
    # ball variables:
    top_b = ball.y_posn
    bottom_b = ball.y_posn + ball.height
    left_b = ball.x_posn
    right_b = ball.x_posn + ball.width
    r = (right_b - left_b)/2
    v_centre_b = top_b + r
    h_centre_b = left_b + r

    if((bottom_b > top) and (top_b < bottom) and (right_b > left) and (left_b < right)):
```
```

*(continues on the next page)*