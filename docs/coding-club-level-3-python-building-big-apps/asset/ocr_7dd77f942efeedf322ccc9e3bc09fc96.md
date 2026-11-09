```
```python
# detect if ball has hit the bats:
bat_L.detect_collision(my_ball)
bat_R.detect_collision(my_ball)

# detect if the ball has hit the left wall:
if(my_ball.x_posn <= 3):
    my_ball.stop_ball()
    my_ball.start_position()
bat_L.start_position()
bat_R.start_position()
my_table.move_item(bat_L.rectangle, 20, 150, 35, 250)
my_table.move_item(bat_R.rectangle, 575, 150, 590, 250)
score_left = score_left + 1
    if(score_left >= 10):
        score_left = "W"
        score_right = "L"
    first_serve = True
    my_table.draw_score(score_left, score_right)

# detect if the ball has hit the right wall:
if(my_ball.x_posn + my_ball.width >= my_table.width - 3):
    my_ball.stop_ball()
    my_ball.start_position()
    bat_L.start_position()
    bat_R.start_position()
    my_table.move_item(bat_L.rectangle, 20, 150, 35, 250)
    my_table.move_item(bat_R.rectangle, 575, 150, 590, 250)
```
```