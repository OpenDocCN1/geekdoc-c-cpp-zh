# Move the fangflower

Unlike other flowers, the fangflowers don’t stay in one place. They move all over the garden trying to zap the cow. In this step, you’ll add the code that generates the velocity of each fangflower along the x-axis and y-axis. The fangflowers will use a combination of these two velocities to move up, down, side to side, or diagonally. Add the following code under def velocity() from Step 29.

![](bbox=[0.059, 0.246, 0.968, 0.751])

> Remember, we talked about velocity on page 160.

This combination of the two velocities affect a fangflower’s movement.

This is one of eight different directions a fangflower can move in.

```
```python
def velocity():
    random_dir = randint(0, 1)
    random_velocity = randint(2, 3)
    if random_dir == 0:
        return -random_velocity
    else:
        return random_velocity
```
```

This generates the velocity of the fangflower with no direction yet.

If the direction is 0, this returns a negative velocity.

This line generates a number that represents the direction of the fangflower.

If the direction is 1, this returns a positive velocity.