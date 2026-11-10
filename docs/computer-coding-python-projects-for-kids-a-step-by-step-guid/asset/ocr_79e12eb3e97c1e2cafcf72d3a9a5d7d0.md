# ## Block a multiple snap

Next add the following line to the snap() function to set the value of previous_color to the empty string ('') after a correct snap. Now if a player presses their key again before the next shape is shown, they will lose a point. This is because '' will never be equal to the current colour, except before the first shape is shown.

> There's nothing I don't know about multiple snaps!

```
```python
shape = c.create_text(200, 200, text='SNAP! You scored 1 point!')
previous_color = ''
```
```

# ## Prevent early snaps

Since previous_color and current_color are equal at the beginning of the game, players can still cheat by pressing their key before the first shape appears. To solve this, set the two variables to different strings at the start. Change their values to 'a' and 'b'.

```
```python
previous_color = 'a'
current_color = 'b'
```
```

> Starting with different strings means that a snap can't be made until the shapes appear on the screen.

# ## Change the messages

If both players press their keys at almost the same time, it might be confusing as to who has scored or lost a point. To fix this, you can change the messages that are displayed when players attempt a snap.

> Don't forget to save your work.

```
```python
if valid:
    if event.char == 'q':
        player1_score = player1_score + 1
        shape = c.create_text(200, 200, text='SNAP! Player 1 scores 1 point!')
    else:
        player2_score = player2_score + 1
        shape = c.create_text(200, 200, text='SNAP! Player 2 scores 1 point!')
    previous_color = ''
else:
    if event.char == 'q':
        player1_score = player1_score - 1
        shape = c.create_text(200, 200, text='WRONG! Player 1 loses 1 point!')
    else:
        player2_score = player2_score - 1
        shape = c.create_text(200, 200, text='WRONG! Player 2 loses 1 point!')
```
```