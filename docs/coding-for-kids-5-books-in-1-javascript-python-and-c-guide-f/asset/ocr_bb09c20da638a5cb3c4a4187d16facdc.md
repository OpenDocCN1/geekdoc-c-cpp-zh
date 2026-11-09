```
```python
# moving ball
import pygame

# frames per second
fps = 50

# Define some colors
white = (255, 255, 255)
red = (255, 0, 0)

# A clock instance so we can control frames per second fps
clock = pygame.time.Clock()

# initialize display surface
screen = pygame.display.set_mode((500, 500))
pygame.display.set_caption("moving ball")

pygame.init()
# white background
screen.fill(white)

# initial ball position at center
x = 250
y = 250

# global x and y so it have access to outer x and y
# right function
def move_right():
    global x

    # if ball is near border reset to center
    if x < 480:
        x = x + 2
    else:
        x = 250
        y = 250
```
```