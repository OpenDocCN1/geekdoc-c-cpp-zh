# random number function

```
```python
# dice game if it is even player 1 point
# odd player 2 gets 1 point
# import random library
import random

# create class player with score initialize to zero
class player:
    score = 0

# if number is even return True else return False
def is_even(n):
    even = None
    if n % 2 == 0:
        even = True
    else:
        even = False

    return even

# create players
player1 = player()
player2 = player()


# run loop for 1000 times
for i in range(1000):
    # dice flip, return random number between 1 and 6 inclusive
    dice = random.randint(1, 6)

    if is_even(dice):
        player1.score += 1
    else:
        player2.score += 1

print("Player 1 score is: ", player1.score)
print("Player 2 score is: ", player2.score)
```
```

randint which generate numbers between 1 and 6 inclusive. Class player creates player objects with score initialized to zero. Each time one player wins we access player.score and increment it by one.

```
```text
Player 1 score is: 518
Player 2 score is: 482
```
```

We can see that players score are close, which is expected since each player win probability is 50% as the ration of odd:even of dice output is 1:1.

# Practice Problems