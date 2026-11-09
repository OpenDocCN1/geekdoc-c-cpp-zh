```
```python
# if guess already made
if guess in guessed :
    print("You have already made this guess\n")

# check input with the character in word
if guess not in country:
    turns -= 1
else:
    # character is in word , append character
    # the number of times it appear in word
    count = country.count(guess)
    for i in range(count):
        guessed.append(guess)

# if guessed length match country length then user wins
# else if ran out of turns user loses
if len(guessed) == len(country):
    print("Congratulation you guessed correctly!!")
    break
elif turns == 0 :
    print("Good luck next time")
```
```

# ## Output:

Guess the characters

You have 4 left.  
guess a character:n  
n----  
You have 4 left.  
guess a character:o  
no---  
You have 4 left.  
guess a character:r  
nor--  
You have 4 left.  
guess a character:w  
norw-  
You have 4 left.  
guess a character:a  
norwa-  
You have 4 left.  
guess a character:f  
norwa-  
You have 3 left.  
guess a character:  
Congratulation you guessed correctly!!

# # Practice Problems

+   1. Write a program to append all dictionary values to a list.