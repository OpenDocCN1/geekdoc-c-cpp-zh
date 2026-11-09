
## 大语言模型

大语言模型（Large Language Model，LLM）是一种基于深度学习的人工智能模型，能够理解和生成自然语言。它通过学习海量文本数据，掌握语言的语法、语义和知识，从而在各种任务中表现出色。

LLM 的能力包括：

- 文本生成
- 问答系统
- 机器翻译
- 代码生成

```python
from transformers import pipeline

generator = pipeline('text-generation', model='gpt2')
output = generator('Hello, world!', max_length=50)
print(output)
```

LLM 的应用场景：

- 智能客服
- 内容创作
- 教育与科研

## Output snapshots

Moving right

![](img/443990a0ec620659ce8be783c0758bc6_630_0.png)

## Example 4 Bouncing ball

In this program we create a ball that keeps bouncing off borders.

What does it mean for a ball to bounce off a border?

Earlier we kept moving the ball by incrementing/decrementing its x and y position by a unit step.

In moving the ball right, we incremented x by 1, while we decremented x by 1 to move it to left. So, to bounce the ball off a given border we need to detect which border it is hitting and increment or decrement the correct coordinate x or y.

In bounce function,

```python
stepx = -1 * stepx  # flip x direction if right or left borders touched
stepy = -1 * stepy  # flip y direction if top or bottom borders touched
```

These lines keep flipping the corresponding coordinate whenever a border is touched.

```python
# bounce function
def bounce():
    global stepx, stepy, x, y

    # right border and left bounce then make horizontal step negative
    if x > 480 or x < 20:
        stepx = -1 * stepx

    # top border and bottom border bounce then make vertical step negative
    if y > 480 or y < 20:
        stepy = -1 * stepy

    # update x and y
    x += stepx
    y += stepy

# game infinite loop
loop = True

while loop:

    # if quit button press event quit
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            loop = False

    pygame.draw.circle(screen, red, (x, y), 20)
    # update frame
    bounce()
    pygame.display.update()
    # update fps frames per second
    clock.tick(fps)

    # clear screen
    screen.fill(white)

pygame.quit()
```

### Output snapshots

Bouncing off the top border.

![](img/443990a0ec620659ce8be783c0758bc6_633_0.png)

bouncing ball

![](img/443990a0ec620659ce8be783c0758bc6_634_0.png)

## Practice Problems

- 1. Modify the growing square so it grows from top left corner instead of center.
- 2. Make a blinking red circle at center that blinks every 2 seconds.
- 3. Create a shrinking circle, where it starts at radius equal to window size and shrinks to radius 10.
- 4. Create 2 bouncing balls where they bounce off borders and also bounce off each other if they collide.
  - Hint: in bounce function check for the distance between balls, if close enough trigger a bounce.

## Handling Keypress and Mouse Click events

Pygame deals with user inputs mainly using the pygame.event module. pygame.event listens and registers all events that come from a keyboard or mouse. Every time an event happens, an event object is created to record it.

In fact, we have been using pygame.event several times in our programs.

In this snippet, in the game loop we continuously check for any new events from pygame.event.

`pygame.event.get()` returns a list of events that occurred since the last `pygame.event.get()` call.

When the quit button is pressed, pygame.event registers this event as an event with a type pygame.QUIT.

So we loop through all events and check if any of the event types is pygame.QUIT; if so, we set the loop variable to false to quit the loop in the next iteration.

```python
# game infinite loop
loop = True
while loop:
    # if quit button press quit
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            loop = False
```

To read more about pygame events refer to this link:

[http://man.hubwiz.com/docset/PyGame.docset/Contents/Resources/Documents/ref/event.html](http://man.hubwiz.com/docset/PyGame.docset/Contents/Resources/Documents/ref/event.html)

This table shows some common pygame.event constants and their attributes.

| Constant name | Attributes |
|---|---|
| QUIT | none |
| ACTIVEEVENT | gain, state |
| KEYDOWN | key, mod |
| KEYUP | key, mod |
| MOUSEMOTION | pos, rel, buttons |
| MOUSEBUTTONUP | pos, button |
| MOUSEBUTTONDOWN | pos, button |

### Keyboard events

KEYUP and KEYDOWN events have attribute key constants representing keyboard keys. Using capital K followed by underscore and key name. For example, F1 is K_F1, w is K_w.

In this snippet, we check when a key is pressed down using pygame.KEYDOWN; we check what arrow key is pressed down and print a message for the key name.

```python
for event in pygame.event.get():
    if event.type == pygame.QUIT:
        pygame.quit()
    elif event.type == pygame.KEYDOWN:
        if event.key == pygame.K_UP:
            print("Player moved up")
        elif event.key == pygame.K_LEFT:
            print("Player moved left")
        elif event.key == pygame.K_DOWN:
            print("Player moved down")
        elif event.key == pygame.K_RIGHT:
            print("Player moved right")
```

To read all key bindings, read the pygame keys documentation on

[https://www.pygame.org/docs/ref/key.html](https://www.pygame.org/docs/ref/key.html)

### Mouse events

There are three types of mouse events in pygame: MOUSEBUTTONDOWN, MOUSEBUTTONUP, and MOUSEMOTION.

MOUSEBUTTONDOWN, MOUSEBUTTONUP, and MOUSEMOTION are received when the user presses or moves a mouse.

They have attributes:

- Button: 1 for left button, 2 for mouse wheel and 3 for right button.
- Pos: Mouse absolute position of mouse (x,y) when button is pressed

MOUSEMOTION is received when the user mouse moves; it has 3 attributes:

- Buttons: tuple of mouse button pressed or not (left, mouse wheel, right)
- Pos: absolute cursor position (x,y) in pixels
- Rel: position relative to previous position (relative_x, relative_y)

In this example, we used the three discussed mouse attributes to detect mouse actions.

```python
# detect mouse actions
for event in pygame.event.get():
    if event.type == pygame.QUIT:
        pygame.quit()
    elif event.type == pygame.MOUSEMOTION:
        if event.rel[0] > 0: # 'rel' is a tuple (x, y). 'rel[0]' is the x-value.
            print("Moving the mouse to the right")
        elif event.rel[1] > 0: # pygame origin is at top left corner so higher y-value means it is further down.
            print("Moving the mouse down")
    elif event.type == pygame.MOUSEBUTTONDOWN:
        if event.button == 1:
            print("Left mouse button pressed")
        elif event.button == 3:
            print("Right mouse button pressed")
    elif event.type == pygame.MOUSEBUTTONUP:
        print("Mouse button released")
```

## Example 1: Moving Square

In this example we implement a moving square similar to the past chapter, but it moves by keyboard keys instead. We detect an event of type pygame.KEYDOWN, then we check for the event.

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

Moving

![](img/443990a0ec620659ce8be783c0758bc6_641_0.png)

## Example: Moving Square by Mouse

In this example, we let the square follow the mouse by updating the square position with the mouse cursor position. We access mouse cursor position with pygame.MOUSEMOTION; mouse x position is event.pos[0] and y position is event.pos[1]. We also change the color of the square if the mouse left button is clicked using pygame.MOUSEBUTTONUP.
