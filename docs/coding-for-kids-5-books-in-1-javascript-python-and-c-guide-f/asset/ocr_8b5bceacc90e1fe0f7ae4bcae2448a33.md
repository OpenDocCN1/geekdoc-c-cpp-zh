# Example 2 Frowny face

In this script we create an angry frowny face. This program is very similar to the last example. Except that we draw different shapes. Frowny face basically consists of a 1 circle for face, 2 circles for eyes and an arc for mouth. To understand arc method, read **pygame** documentation. Try to understand how arc gets oriented, you will need it in the practice problems.

```
```python
# import pygame module
import pygame
import math

# activate a pygame library inst .
pygame.init()

# define the RGB value some colors
white = (255, 255, 255)
yellow = (255, 255, 0)
red = (255, 0, 0)

# assigning width 600 , height 600 to background
dimensions = (300, 300)

# create the display surface object
display = pygame.display.set_mode(dimensions)

# naming window name
pygame.display.set_caption("Frowny face !")

# Display color is white
display.fill(white)

# Draw face
pygame.draw.circle(display, yellow, (150, 150), 50, 0)

# Draw left eye
pygame.draw.circle(display, red, (130, 140), 10, 0)

# Draw right eye
pygame.draw.circle(display, red, (170, 140), 10, 0)
```
```