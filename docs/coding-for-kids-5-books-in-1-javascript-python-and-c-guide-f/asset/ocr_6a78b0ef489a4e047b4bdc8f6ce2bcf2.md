```
```python
import pygame
import sys
pygame.init()
fps=30
fpsclock=pygame.time.Clock()
surface=pygame.display.set_mode((500, 500))
pygame.display.set_caption("Moving Square")
white=(255,255,255)
x=10
y=10
step=5
while True:
    surface.fill(white)
    pygame.draw.rect(surface, (255,0,0), (x, y, 70, 65))
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            pygame.quit()
            sys.exit()
        elif event.type == pygame.KEYDOWN:
            if event.key == pygame.K_LEFT:
                x -= step
            elif event.key == pygame.K_UP:
                y -= step
            elif event.key == pygame.K_RIGHT:
                x += step
            elif event.key == pygame.K_DOWN:
                y += step
    pygame.display.update()
    fpsclock.tick(fps)
```
```