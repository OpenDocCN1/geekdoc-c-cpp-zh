# Project reference

Here you’ll find the complete Python code for every project in this book, except for the hacks and tweaks. If your projects don’t run properly, carefully check your scripts against the code shown here.

# Animal Quiz (page 36)

```
```python
def check_guess(guess, answer):
    global score
    still_guessing = True
    attempt = 0
    while still_guessing and attempt < 3:
        if guess.lower() == answer.lower():
            print('Correct Answer')
            score = score + 1
            still_guessing = False
        else:
            if attempt < 2:
                guess = input('Sorry wrong answer. Try again ')
                attempt = attempt + 1

    if attempt == 3:
        print('The correct answer is ' + answer)

score = 0
print('Guess the Animal')
guess1 = input('Which bear lives at the North Pole? ')
check_guess(guess1, 'polar bear')
guess2 = input('Which is the fastest land animal? ')
check_guess(guess2, 'cheetah')
guess3 = input('Which is the largest animal? ')
check_guess(guess3, 'blue whale')

print('Your score is ' + str(score))
```
```

# Password Picker (page 52)

```
```python
import random
import string

adjectives = ['sleepy', 'slow', 'smelly',
              'wet', 'fat', 'red',
              'orange', 'yellow', 'green',
              'blue', 'purple', 'fluffy']
```
```