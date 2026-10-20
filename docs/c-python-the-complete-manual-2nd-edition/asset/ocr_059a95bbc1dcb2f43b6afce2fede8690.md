# # Beginner Python Mistakes

# ## COUNTING LOOPS

Remember that in Python a loop doesn't count the last number you specify in a range. So if you wanted the loop to count from 1 to 10, then you will need to use:

```
n = list(range(1, 11))
```

![](bbox=[0.05, 0.3, 0.48, 0.55])

# ## COLONS

It’s common for beginners to forget to add a colon to the end of a structural statement, such as:

```
class Hangman:
    def __init__(self, word):
        self.word = word
        self.missed_letters = []
        self.guessed_letters = []

def guess(self, letter):
    if letter not in self.word and letter not in self.guessed_letters:
        self.guessed_letters.append(letter)
    elif letter not in self.word and letter not in self.missed_letters:
        self.missed_letters.append(letter)
    else:
        return False
    return True

def hangman_over(self):
    return self.hangman_won() or (len(self.missed_letters) == 6)

def hangman_won(self):
    if '-' not in self.hide_word():
        return True
    return False

def hide_word(self):
    rtn = ''
    for letter in self.word:
        if letter not in self.guessed_letters:
            rtn += ' '
        else:
            rtn += letter
    return rtn
```

# ## CASE SENSITIVE

Python is a case sensitive programming language, so you will need to check any variables you assign. For example, Lives=10 is a different variable to lives=10, calling the wrong variable in your code can have unexpected results.

```
Lives=10
lives=9
print(Lives, lives)
```

![](bbox=[0.05, 0.76, 0.48, 0.95])

# ## BRACKETS

Everyone forgets to include that extra bracket they should have added to the end of the statement. Python relies on the routine having an equal amount of closed brackets to open brackets, so any errors in your code could be due to you forgetting to count your brackets; including square brackets.

```
def print_game_status(self):
    print (board[len(self.missed_letters)])
    print ('Word: ' + self.hide_word())
    print ('Letters Missed: ')
    for letter in self.missed_letters:
        print (letter,)
    print ()
    print ('Letters Guessed: ')
    for letter in self.guessed_letters:
        print (letter,)
    print ()
```

# ## OPERATORS

Using the wrong operator is also a common mistake to make. When you’re performing a comparison between two values, for example, you need to use the equality operator (a double equals, ==). Using a single equal (=) is an assignment operator that places a value to a variable (such as, lives=10).

```
b = 5
c = 10
d = 10
b == c #false because 5 is not equal to 10
c == d #true because 10 is equal to 10
```

# ## OPERATING SYSTEMS

Writing code for multiple platforms is difficult, especially when you start to utilise the external commands of the operating system. For example, if your code calls for the screen to be cleared, then for Windows you would use cls. Whereas, for Linux you need to use clear. You need to solve this by capturing the error and issuing it with an alternative command.

```
# Code to detect error for using a different OS
run=1
while (run==1):
    try:
        os.system('clear')
    except OSError:
        os.system('cls')
print("\n>>>>>>>>>>>>>>Python 3 File Manager<<<<<<<<<<<<<\n")
```