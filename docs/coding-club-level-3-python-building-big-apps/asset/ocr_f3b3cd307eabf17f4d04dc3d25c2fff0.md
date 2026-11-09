# Final steps

table.py is complete. Now save it and re-open main.py. There is nothing much to do here except add the scoring functionality (the rules) in three places:

+   - when the game is started we want to set the scores to zero
+   - when the ball hits the left wall we want to add one to the right player's score
+   - when the ball hits the right wall we want to add one to the left player's score.

Copy in the new code indicated in Code Box 6.9, which shows the complete code for main.py. If all goes well you should have a fully functioning game – with a scoreboard.

```
```python
from tkinter import *
import table, ball, bat

# initialise global variables
x_velocity = 10
y_velocity = 0
score_left = 0
score_right = 0
first_serve = True
```
```