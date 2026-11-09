
```python
# Draw right eye
pygame.draw.circle(display, red, (170, 140), 10, 0)

# Draw mouth using arc
# arc(surface, color, bounding_rect, start_angle, stop_angle, width=1)
pygame.draw.arc(display, red, (135, 175, 30, 20), 0, math.pi, width=1)

# infinite loop to keep session on
while True:
    # Iterate over the list of Event objects
    # that gets returned by pygame.event.get() method.
    for event in pygame.event.get():

        # if event object type is QUIT with corner exit button is clicked
        # then quitting pygame and program
        if event.type == pygame.QUIT:

            # quit pygame session
            pygame.quit()
            # quit the program
            quit()

    # Draws the objects screen.
    pygame.display.update()
```

## Output:

😟 Frowny face!

![](img/443990a0ec620659ce8be783c0758bc6_614_0.png)

## Practice Problems

- 1. Use frowny face program discussed earlier and turn it into smiley face instead.
- 2. Create a display of 800 by 800 and create 4 sides connected red borders and a circle centered at center where it is circumscribed by the borders.
- 3. Pick 4 of your favorite emojis and try to draw them using pygame.
- 4. Create a shape similar to Football pitch picture below.

![](img/443990a0ec620659ce8be783c0758bc6_615_0.png)

## Animations in Pygame

Animations are images manipulated to appear as moving pictures. To make an animation we create many continuous pictures/shapes and view them continuously. The number of times we update the screen is called Frames per second (fps); fps is the number of frames/pictures shown per second. Greater fps numbers make the transitions in videos/games smoother thus increasing the quality. The game loop discussed in earlier chapter is responsible for updating the state of game at fps frames per second. This is how games are made, updating the screen continuously with pictures at a rate human eyes can’t distinguish that pictures are in fact discrete. The figure below shows multiple frames of a running horse. Grouping these frames will result in a running horse video.

![](img/443990a0ec620659ce8be783c0758bc6_617_0.png)

*The famous horse in motion*

## Growing square

We make a square that grows in size until it fills the entire lower right screen quadrant. The logic is very similar to how we made various shapes in the previous example except for 2 main differences. We make pygame clock instance `clock=pygame.time.Clock()`, this is a pygame method to keep track of time. We use it in the program to control how many frames per second (fps) we want using `clock.tick(fps)`. Faster fps updates the shape more frequently which makes the square grow faster.

The second difference is that square side is not fixed anymore. Every loop iteration the square side is increased using `side = 1.01 * side`, the screen is cleared (filled with white color) using `screen.fill(white)` and a new square with the new side size is drawn. Experiment with the value 1.01, observe how increasing/decreasing this value affects the animation speed.

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

### Output snapshots:

Growing square

Growing square

Growing square

Growing square

## Growing circle

This example is very similar to growing square example. Except that we draw a circle instead of square and increase the radius instead of side length.

```python
# growing circle
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
pygame.display.set_caption("Growing circle")

pygame.init()
# white background
screen.fill(white)

# game infinite loop
loop = True

# initial circle radius
rad = 50

while loop:
    # if quit button press event quit
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            loop = 0

    pygame.draw.circle(screen, red, (250, 250), rad)
    # update frame
    pygame.display.update()

    # update fps frames per second
    clock.tick(fps)

    rad = 1.01 * rad
    # clear screen
    screen.fill(white)

pygame.quit()
```

### Output snapshots:

![](img/443990a0ec620659ce8be783c0758bc6_623_0.png)

![](img/443990a0ec620659ce8be783c0758bc6_623_1.png)

![](img/443990a0ec620659ce8be783c0758bc6_623_2.png)

## Moving a ball in different direction

In this example we move a ball in 4 different directions using move_right, move_left, move_up, and move_down functions. The logic is similar to previous examples, instead of growing shape size every frame we ‘grow’ object position each time. The ball starts in the center and keeps moving until it hits a border where it restarts from center again. move_right() function works by updating the ball coordinates. The function does not take any inputs because it accesses x and y directly in the global scope because x and y are defined as a global variable. With each function call the x coordinate is incremented by step size of 2 pixels. The step size determines how smooth the shape moves. The function makes sure the ball is near border by never incrementing x beyond 480. The background surface size is 500. If x > 480 the ball position is reset to center.

```python
# global x and y so it have access to outer x and y
# right function
def move_right():
    global x, y

    # if ball is near border reset to center
    if x < 480:
        x = x + 2
    else:
        x = 250
        y = 250
```

Other functions move_left, move_up, and move_down are implemented similarly but with changing whether x and y is incremented and detecting a different border. Read the code below carefully and try to understand it.

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
    global x, y

    # if ball is near border reset to center
    if x < 480:
        x = x + 2
    else:
        x = 250
        y = 250

# move left
def move_left():
    global x, y

    # if ball is near border reset to center
    if x > 20:
        x = x - 2
    else:
        x = 250
        y = 250

# move up
def move_up():
    global x, y

    # if ball is near border reset to center
    if y > 20:
        y = y - 2
    else:
        x = 250
        y = 250

# move down
def move_down():
    global x, y

    # if ball is near border reset to center
    if y < 480:
        y = y + 2
    else:
        x = 250
        y = 250

# game infinite loop
loop = True
```
