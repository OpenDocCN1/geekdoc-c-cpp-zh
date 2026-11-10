# ## 6 Store the clue

Now create another list to hold the clue. Unknown letters are stored as question marks. These will be replaced when the player guesses a letter correctly. At the start of the game, the whole list is question marks. You could write it as clue = list['?', '?', '?', '?', '?'], typing one question mark for each letter in the secret word, but the code below is a faster way to write it. Add this line after the secret_word variable.

```
```python
secret_word = random.choice(words)
clue = list('??????')
```
```

The five question marks are stored as a list in the variable clue.

![](bbox=[0.07, 0.35, 0.43, 0.47])

# ## 7 Show the lives left

This project uses the Unicode heart character to display how many lives are left. To make your program easier to read and write, add the next line of code to store the character in a variable.

```
```python
clue = list('??????')
heart_symbol = u'\u2764'
```
```

# ## 8 Remember the result

Now make a variable to store whether or not the player has guessed the word correctly. The variable is set as False to begin with because the player doesn't know the word when the game starts. Type this line below the code for the heart symbol.

```
```python
heart_symbol = u'\u2764'
guessed_word_correctly = False
```
```

This is a Boolean (True or False) value.

# ### EXPERT TIPS

# ### Word length

Be careful to only add words that are five letters long. The list that stores the clue only has room for five characters. If you add words of more than five letters, you'll see an error message when the program tries to enter any letters past the fifth one in the clue.

```
```text
Index error: list assignment index
out of range
```
```

If you try to add words that are less than five letters long, the program will work, but the player will still see five question marks. They'll think that the answer has to be five letters long. For example, if you used "car", the program would look like this.

```
```text
['?', '?', '?', '?', '?']
Lives left: ❤❤❤❤❤
Guess a letter or the whole word: c
['c', '?', '?', '?', '?']
Lives left: ❤❤❤❤❤
Guess a letter or the whole word: a
['c', 'a', '?', '?', '?']
Lives left: ❤❤❤❤❤
Guess a letter or the whole word: r
['c', 'a', 'r', '?', '?']
Lives left: ❤❤❤❤❤
Guess a letter or the whole word:
```
```

The last two question marks don't represent any letters, so they never disappear.

The player could never win, because the last two question marks would remain no matter what letter they guessed!