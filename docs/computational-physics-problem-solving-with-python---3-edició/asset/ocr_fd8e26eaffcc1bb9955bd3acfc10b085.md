![](bbox=[0.18, 0.11, 0.85, 0.42])

# Figure 2.2

A flowchart illustrating a program to compute projectile motion. Plot (a) shows the basic components of the program, and plot (b) shows are some of its details. When writing a program, first map out the basic components, then decide upon the structures, and finally fill in the details. This is called top-down programming.

+   6. Revise Area.py so that it takes input from a file name that you have made up, then writes in a different format to another file you have created, and then reads from the latter file.
+   7. See what happens when the data type used for output does not match the type of data in the file (e.g., floating point numbers are read in as integers).
+   8. Revise AreaMod so that it uses a main method (which does the input and output) and a separate function or method for the calculation. Check that you obtain the same answers as before.

# Listing 2.2

AreaFormatted.py does I/O to and from keyboard, as well as from a file. It works with either Python 2 or 3 by switching between raw_input and input. Note to read from a file using Canopy, you must right click in the Python run window and choose Change to Editor Directory.

```
# AreaFormatted: Python 2 or 3 formated output, keyboard input, file input
from numpy import *
from sys import version
if int(version[0]) >2:               # Python 3 uses input, not
    raw_input
    raw_input=input
name = raw_input('Key in your name: ')          # raw_input strings
print("Hi",name)
radius = eval(raw_input('Enter a radius: '))    # For numerical values
print('you entered radius= %8.5f'%radius)       # formatted output
print('Enter new name and r in file Name.dat')  # raw_input strings
infile = open('Name.dat','r')                   # Read from file Name.dat
```