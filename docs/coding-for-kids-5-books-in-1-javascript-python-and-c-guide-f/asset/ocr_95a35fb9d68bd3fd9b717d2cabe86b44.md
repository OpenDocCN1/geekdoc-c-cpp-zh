```
```python
while loop:
    # detect pressed keys
    keys = pygame.key.get_pressed()

    # if quit button press event quit
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            loop = 0

    # get mouse pointer coordinates
    x, y = pygame.mouse.get_pos()

    # move the ball by a step
    move_ball()
    # draw ball
    ball()
    # draw paddle at mouse x coordinate
    paddle(x, 490)
    # is the ball served
    served()
    # update frame
    pygame.display.update()
    # white background
    screen.fill(white)
    # update fps frames per second
    clock.tick(fps)

pygame.quit()
```
```

```
```python
# Draw the ball at x_ball, y_ball
def ball():
    pygame.draw.circle(screen, red, (x_ball, y_ball), 10, 10)

# draw paddle at x, y
def paddle(x,y):
    pygame.draw.rect(screen, black, (x, y, 80, 10))

# move ball by a step
def move_ball():
    global x_ball, y_ball, horizontal_direction, vertical_direction
    # if ball is going to left decrement x_ball so it continues left
    if horizontal_direction == "left":
        x_ball -= step

        # if ball is near left border reflect to right
        if x_ball < 10:
            horizontal_direction = "right"

    # if ball is going downward increment y_ball so it continues downward
    if vertical_direction == "down":
        y_ball += step

    # if ball is going upward decrement y_ball so it continues upward
    if vertical_direction == "up":
        y_ball -= step

        # if ball is near upper border reflect downward
        if y_ball < 10:
            vertical_direction = 'down'

    # if ball is going right increment x_ball so it continues right
    if horizontal_direction == "right":
        x_ball += step
```
```