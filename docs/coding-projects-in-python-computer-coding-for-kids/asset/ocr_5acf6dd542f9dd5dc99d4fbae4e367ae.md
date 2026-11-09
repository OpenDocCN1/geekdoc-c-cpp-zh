# Using a dictionary

A dictionary is another way you can store information in Python. It is similar to a list, but each item has two parts: a key and a value. You can test it out by typing this into the shell window.

```
favorite_foods = {'Simon': 'pizza', 'Jill': 'pancakes', 'Roger': 'custard'}
```

This is the key.

This is the value.

A colon is used immediately after the key.

Each item in the dictionary is separated by a comma.

Dictionaries use curly brackets.

▽ 1. To show the contents of a dictionary, you have to print it. Try printing `favorite_foods`.

```
print(favorite_foods)
```

Type this in the shell and hit return.

▽ 2. Now add a new item to the dictionary: Julie and her favorite food. She likes cookies.

```
favorite_foods['Julie'] = 'cookies'
```

Key

Value

▽ 3. Jill has changed her mind—her favorite food is now tacos. You can update this information in the dictionary.

```
favorite_foods['Jill'] = 'tacos'
```

Updated value

▽ 4. Finally, you can look up Roger’s favorite food in the dictionary by simply using his name as the key.

```
print(favorite_foods['Roger'])
```

Use the key to look up the value.

# It’s function time!

The next stage of the project involves creating the functions that you’ll need to use in your program.

# 8  File input

You need a function to read in all the information stored in your text file. It will be similar to the one you used in Countdown Calendar to read in data from your events file. Add this code after the Tkinter import line.

![](bbox=[0.099, 0.832, 0.466, 0.996])

```
from tkinter import Tk, simpledialog, messagebox

def read_from_file():
    with open('capital_data.txt') as file:
```

This line opens the text file.