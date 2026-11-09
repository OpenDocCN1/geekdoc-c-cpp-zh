
## 技巧与调整

**为任务增加更多挑战，让游戏更加引人入胜。**  
**以下是一些可以帮助你上手的想法。**

```python
if keyboard.d:
    hero2.x += MOVE_DISTANCE
    if hero2.x > WIDTH:
        hero2.x = WIDTH
elif keyboard.a:
    hero2.x -= MOVE_DISTANCE
    if hero2.x < 0:
        hero2.x = 0
elif keyboard.s:
    hero2.y += MOVE_DISTANCE
    if hero2.y > HEIGHT:
        hero2.y = HEIGHT
elif keyboard.w:
    hero2.y -= MOVE_DISTANCE
    if hero2.y < 0:
        hero2.y = 0
```

![](img/3188b147f991a51de14dcd2bb4b4c42e_196_0.png)

> 我需要一些帮助！

### 添加另一个英雄

收集这么多蛋，对一个英雄来说可是个大工程。你可以添加另一个英雄来帮忙。为此，你需要添加一些新代码，并修改一些现有代码。首先，改变当前英雄的起始位置，并为新英雄添加一个不同的起始位置。然后，在 draw() 函数中添加一些代码，在屏幕上绘制第二个英雄。现在，将此处显示的代码添加到 update() 函数中，这会让第二个英雄使用一组新按键——W、A、S、D——在屏幕上移动。最后，记得为所有检查碰撞的函数添加一个参数，以便它们同时检查两个英雄的碰撞。

这会让第二个英雄向下移动。

### 让龙更难以预测

目前，预测龙何时醒来相当容易。你可以为每条龙的睡眠周期加入随机因素，让游戏更具挑战性。为此，你首先需要在程序顶部导入 random 模块。然后，你需要在 update_sleeping_dragon() 函数中添加一些代码。这样，每次调用该函数时，都会随机决定是否唤醒龙。为此，请将此处以黑色显示的代码行添加到步骤 23 中。

![](img/3188b147f991a51de14dcd2bb4b4c42e_196_1.png)

> 我知道龙接下来什么时候会醒来。
>
> 它们可没你想的那么可预测。

```python
if lair["sleep_counter"] > lair["sleep_length"]:
    if random.choice([True, False]):
        lair["dragon1"].image = "dragon-awake"
```

## 参考

![](img/3188b147f991a51de14dcd2bb4b4c42e_198_0.png)

## 项目参考

本节包含本书中每个游戏的完整 Python 代码，但不包括技巧与调整部分。如果你的游戏无法正常运行，请对照此处展示的代码仔细检查脚本。

### 射击水果（第 48 页）

```python
from random import randint
apple = Actor("apple")


def draw():
    screen.clear()
    apple.draw()


def place_apple():
    apple.x = randint(10, 800)
    apple.y = randint(10, 600)


def on_mouse_down(pos):
    if apple.collidepoint(pos):
        print("Good shot!")
        place_apple()
    else:
        print("You missed!")
        quit()


place_apple()
```

### 收集硬币（第 58 页）

```python
from random import randint

WIDTH = 400
HEIGHT = 400
score = 0
game_over = False

fox = Actor("fox")
fox.pos = 100, 100

coin = Actor("coin")
coin.pos = 200, 200

def draw():
    screen.fill("green")
    fox.draw()
    coin.draw()
    screen.draw.text("Score: " + str(score), color="black", topleft=(10, 10))

    if game_over:
        screen.fill("pink")
        screen.draw.text("Final Score: " + str(score), topleft=(10, 10), fontsize=60)

def place_coin():
    coin.x = randint(20, (WIDTH - 20))
    coin.y = randint(20, (HEIGHT - 20))

def time_up():
    global game_over
    game_over = True

def update():
    global score

    if keyboard.left:
        fox.x = fox.x - 2
    elif keyboard.right:
        fox.x = fox.x + 2
    elif keyboard.up:
        fox.y = fox.y - 2
    elif keyboard.down:
        fox.y = fox.y + 2

    coin_collected = fox.colliderect(coin)

    if coin_collected:
        score = score + 10
        place_coin()

clock.schedule(time_up, 7.0)
place_coin()
```

### 按数字顺序连线（第 68 页）

```python
from random import randint

WIDTH = 400
HEIGHT = 400

dots = []
lines = []

next_dot = 0

for dot in range(0, 10):
    actor = Actor("dot")
    actor.pos = randint(20, WIDTH - 20), \
    randint(20, HEIGHT - 20)
    dots.append(actor)

def draw():
    screen.fill("black")
    number = 1
    for dot in dots:
        screen.draw.text(str(number), \
                         (dot.pos[0], dot.pos[1] + 12))
        dot.draw()
        number = number + 1
    for line in lines:
        screen.draw.line(line[0], line[1], (100, 0, 0))

def on_mouse_down(pos):
    global next_dot
    global lines
    if dots[next_dot].collidepoint(pos):
        if next_dot:
            lines.append((dots[next_dot - 1].pos, dots[next_dot].pos))
            next_dot = next_dot + 1
        else:
            lines = []
            next_dot = 0
```

### 红色警报（第 80 页）

```python
import random

FONT_COLOR = (255, 255, 255)
WIDTH = 800
HEIGHT = 600
CENTER_X = WIDTH / 2
CENTER_Y = HEIGHT / 2
CENTER = (CENTER_X, CENTER_Y)
FINAL_LEVEL = 6
START_SPEED = 10
COLORS = ["green", "blue"]

game_over = False
game_complete = False
current_level = 1
stars = []
animations = []

def draw():
    global stars, current_level, game_over, game_complete
    screen.clear()
    screen.blit("space", (0, 0))
    if game_over:
        display_message("GAME OVER!", "Try again.")
    elif game_complete:
        display_message("YOU WON!", "Well done.")
    else:
        for star in stars:
            star.draw()

def update():
    global stars
    if len(stars) == 0:
        stars = make_stars(current_level)

def make_stars(number_of_extra_stars):
    colors_to_create = get_colors_to_create(number_of_extra_stars)
    new_stars = create_stars(colors_to_create)
    layout_stars(new_stars)
    animate_stars(new_stars)
    return new_stars

def get_colors_to_create(number_of_extra_stars):
    colors_to_create = ["red"]
    for i in range(0, number_of_extra_stars):
        random_color = random.choice(COLORS)
        colors_to_create.append(random_color)
    return colors_to_create

def create_stars(colors_to_create):
    new_stars = []
    for color in colors_to_create:
        star = Actor(color + "_star")
        new_stars.append(star)
    return new_stars

def layout_stars(stars_to_layout):
    number_of_gaps = len(stars_to_layout) + 1
    gap_size = WIDTH / number_of_gaps
    random.shuffle(stars_to_layout)
    for index, star in enumerate(stars_to_layout):
        new_x_pos = (index + 1) * gap_size
        star.x = new_x_pos

def animate_stars(stars_to_animate):
    for star in stars_to_animate:
        duration = START_SPEED - current_level
        star.anchor = ("center", "bottom")
        animation = animate(star, duration=duration, on_finished=handle_game_over, y=HEIGHT)
        animations.append(animation)

def handle_game_over():
    global game_over
    game_over = True

def on_mouse_down(pos):
    global stars, current_level
    for star in stars:
        if star.collidepoint(pos):
            if "red" in star.image:
                red_star_click()
            else:
                handle_game_over()

def red_star_click():
    global current_level, stars, animations, game_complete
    stop_animations(animations)
    if current_level == FINAL_LEVEL:
        game_complete = True
    else:
        current_level = current_level + 1
        stars = []
        animations = []

def stop_animations(animations_to_stop):
    for animation in animations_to_stop:
        if animation.running:
            animation.stop()

def display_message(heading_text, sub_heading_text):
    screen.draw.text(heading_text, fontsize=60, center=CENTER, color=FONT_COLOR)
    screen.draw.text(sub_heading_text,
                     fontsize=30,
                     center=(CENTER_X, CENTER_Y + 30),
                     color=FONT_COLOR)
```

### 大型问答（第 98 页）

```python
WIDTH = 1280
HEIGHT = 720

main_box = Rect(0, 0, 820, 240)
timer_box = Rect(0, 0, 240, 240)
answer_box1 = Rect(0, 0, 495, 165)
answer_box2 = Rect(0, 0, 495, 165)
answer_box3 = Rect(0, 0, 495, 165)
answer_box4 = Rect(0, 0, 495, 165)

main_box.move_ip(50, 40)
timer_box.move_ip(990, 40)
answer_box1.move_ip(50, 358)
answer_box2.move_ip(735, 358)
answer_box3.move_ip(50, 538)
answer_box4.move_ip(735, 538)
answer_boxes = [answer_box1, answer_box2, answer_box3, answer_box4]

score = 0
time_left = 10

q1 = ["What is the capital of France?",
      "London", "Paris", "Berlin", "Tokyo", 2]

q2 = ["What is 5+7?",
      "12", "10", "14", "8", 1]

q3 = ["What is the seventh month of the year?",
      "April", "May", "June", "July", 4]

q4 = ["Which planet is closest to the Sun?",
      "Saturn", "Neptune", "Mercury", "Venus", 3]

q5 = ["Where are the pyramids?",
      "India", "Egypt", "Morocco", "Canada", 2]

questions = [q1, q2, q3, q4, q5]
question = questions.pop(0)

def draw():
    screen.fill("dim grey")
    screen.draw.filled_rect(main_box, "sky blue")
    screen.draw.filled_rect(timer_box, "sky blue")

    for box in answer_boxes:
        screen.draw.filled_rect(box, "orange")
```
