```
```python
# growing square
import pygame

# frames per second to control speed
fps = 50

# Define some colors
white = (255, 255, 255)
red = (255, 0, 0)

# A clock instance so we can control frames per second fps
clock = pygame.time.Clock()

# initialize display surface
screen = pygame.display.set_mode((500, 500))
pygame.display.set_caption("Growing square")

pygame.init()
# white background
screen.fill(white)

# initial square side length
side = 50

# game infinite loop
loop = True
while loop:

    # if quit button press event quit
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            loop = 0

    pygame.draw.rect(screen, red, (250, 250, side, side))

# update frame
pygame.display.update()

# update fps frames per second
clock.tick(fps)

side = 1.01 * side
# clear screen
screen.fill(white)


pygame.quit()
```
```

# Output snapshots: