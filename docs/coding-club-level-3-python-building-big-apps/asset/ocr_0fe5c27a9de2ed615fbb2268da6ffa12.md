```
```python
# order a defender from the bat class
bat_B = bat.Bat(table=my_table, width=50, height=30, x_posn=250, y_posn=350, colour="blue")

# order invaders from the bat class and start them moving to the right
invaders = []
rows=0
gap=30
colour = ("green", "orange", "yellow", "purple")
while rows < 5:
    n=1
    while n < 7:
        i=80
        invader = bat.Bat(table=my_table, width=50, height=20, x_speed=3, y_speed=15,
                          x_posn=(n*i), y_posn=25+(rows*gap), colour=colour[(rows-1) % 4])
        invaders.append(invader)
        n = n+1
    rows = rows+1

#### Functions:
def game_flow():
    global first_serve
    global direction
    game_over = False
    # wait for first serve:
    if(first_serve == True):
        my_ball.stop_ball()
        first_serve = False
```
```