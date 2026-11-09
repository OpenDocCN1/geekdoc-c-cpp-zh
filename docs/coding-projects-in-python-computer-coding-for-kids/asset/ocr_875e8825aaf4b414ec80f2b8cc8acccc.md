# ## 13 Give the player more chances

The player currently has only one chance to get the answer right. You can make it a bit easier for them by giving them three chances to answer a question. Change the `check_guess()` function to look like this.

Don't forget to save your work.

```
```python
def check_guess(guess, answer):
    global score
    still_guessing = True
    attempt = 0
    while still_guessing and attempt < 3:
        if guess.lower() == answer.lower():
            print('Correct answer')
            score = score + 1
            still_guessing = False
        else:
            if attempt < 2:
                guess = input('Sorry wrong answer. Try again. ')
            attempt = attempt + 1

    if attempt == 3:
        print('The correct answer is ' + answer)

score = 0
```
```

This variable will hold one of only two values: True or False.

A `while` loop runs the check code three times or until the player gets the answer correct—whichever comes first.

Make sure each line of code has the correct indent.

The `else` variable asks the player to enter another answer if they get it wrong.

Add 1 to the number of guesses the player has had.

This code displays the correct answer after three wrong guesses.

# ## How it works

To know if the player has gotten the right answer, you need to create a variable called `still_guessing`. You then set the variable to `True` to show that the right answer hasn't been found yet. It's set to `False` when the player gets the right answer.

Largest animal? I don't know. Give me three guesses!

![](bbox=[0.26, 0.7, 0.9, 0.9])