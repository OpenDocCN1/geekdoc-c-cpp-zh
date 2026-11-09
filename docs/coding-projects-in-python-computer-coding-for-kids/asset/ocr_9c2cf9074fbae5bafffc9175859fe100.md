# ## Setting up

You’ll build Nine Lives in two stages. First you’ll import the module you need for the program and create several variables. Then you’ll write the main code for the program.

![](bbox=[0.622, 0.078, 0.965, 0.238])

+   1. **Create a new file**
+   
+   Open IDLE and create a new file. Save it as “nine lives.py”.

![](bbox=[0.108, 0.321, 0.387, 0.419])

+   2. **Import the module**
+   
+   This project uses Python’s random module, so start by typing the line of code shown here to import it.

```
```python
import random
```
```

+   3. **Make a variable**
+   
+   Below the import line, create a variable called `lives` to keep track of the number of lives (guesses) the player has left.

```
```python
import random

lives = 9
```
```

The player starts with nine lives.

+   4. **Make a list**
+   
+   The program will only know the words that you give it. You’ll need to put these words in a list, therefore the list in a variable called `words`. Add this line beneath your `lives` variable.

```
```python
lives = 9
words = ['pizza', 'fairy', 'teeth', 'shirt',
         'otter', 'plane']
```
```

Each item in the list is a string made up of five characters.

+   5. **Choose a secret word**
+   
+   At the start of each game, the program will randomly pick the word that the player has to guess and store it in a variable called `secret_word`. Add a line to create this new variable.

```
```python
words = ['pizza', 'fairy', 'teeth', 'shirt',
         'otter', 'plane']
secret_word = random.choice(words)
```
```

This variable uses the random module’s choice function.

![](bbox=[0.143, 0.846, 0.753, 0.999])