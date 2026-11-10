# Password Picker flowchart

The program randomly selects each of the password’s four parts, puts them together, and displays the password in the shell window. If you want another password, it repeats those steps again. If you don’t, the program ends.

+   - Start
+   - Choose a random adjective
+   - Choose a random noun
+   - Choose a random number between 0 and 100
+   - Choose a random punctuation character
+   - Create the secure password
+   - Display the secure password
+   - Want another password?
+     - Y: Repeat the password-generation steps
+     - N: End

# How it works

This project will show you how to use Python’s random module. The program uses random choices from groups of adjectives, nouns, numbers, and punctuation characters to assemble each password. You’ll soon be making crazy, hard-to-forget passwords, such as “fluffyapple14(“ or “smellygoat&”!

![](bbox=[0.435, 0.24, 0.951, 0.374])

# Clever yet simple!

The program does clever things with passwords, but there isn’t a lot of code in it, so it won’t take long to make.

![](bbox=[0.68, 0.415, 0.958, 0.649])

+   1. **Create a new file**
+      Open IDLE. Under the File menu, select New File. Save the file as “password_picker.py”.
+   2. **Add the modules**
+      Import the string and random modules from the Python library. Type these two lines at the top of your file, so you can use the modules later.
+   3. **Welcome the user**
+      First create a message to welcome the user to the program.

```
import random
import string
```

The string module lets you do useful things with strings, like splitting them apart or changing the way they appear.

This line shows a message to welcome the user.

```
import random
import string

print('Welcome to Password Picker!')
```