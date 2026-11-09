# ## 28 Dragon collisions

If the hero gets too close to an awake dragon, the player will lose a life. You’ll use the `check_for_dragon_collision()` function to calculate this distance. Add this code under what you typed in Step 27.

![](bbox=[0.684, 0.061, 0.805, 0.185])

```
```python
check_for_dragon_collision(lair)

def check_for_dragon_collision(lair):
    x_distance = hero.x - lair["dragon"].x
    y_distance = hero.y - lair["dragon"].y
    distance = math.hypot(x_distance, y_distance)
    if distance < ATTACK_DISTANCE:
        handle_dragon_collision()
```
```

This calculates the horizontal and vertical distances between the dragon and the hero.

This finds the distance between the dragon and the hero in a straight line.

This function is called if the distance between the hero and dragon is less than ATTACK_DISTANCE.

# ## 29 Reset hero

If the player loses a life, the hero’s position needs to be reset to the starting position. You’ll use the `animate()` function to do this. In your game, this function takes three parameters—the hero Actor, the hero’s starting position, and the subtract_life() function. Add the code shown in black here.

![](bbox=[0.535, 0.464, 0.978, 0.721])

```
```python
distance = math.hypot(x_distance, y_distance)
if distance < ATTACK_DISTANCE:
    handle_dragon_collision()
```
```

```
```python
def handle_dragon_collision():
    global reset_required
    reset_required = True
    animate(hero, pos=HERO_START, on_finished=subtract_life)
```
```

This function is called when the animation is complete.