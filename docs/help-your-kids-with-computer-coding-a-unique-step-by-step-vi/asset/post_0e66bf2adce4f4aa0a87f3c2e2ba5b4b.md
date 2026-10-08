
# BUGS AND DEBUGGING 149

# Add a "print" and "input(i)"

The program doesn't show what it's doing at each step. Adding a "print" command will help you see what's happening. The "input()" command waits for the "return" or "Enter" key to be pressed before looping.

```python
top_num = 5
total = 0
for n in range(top_num):
    total = total + n
    print('DEBUG: n=', n, 'total=', total)
    input(0)
print('Sum of numbers 1 to', top_num, 'is', total)
```

The total() command prints the current value of the loop and the variable so far

![](img/72d218a7a73c4d4abc7be582ebd85385_150_0.png)

# New output

The loop is only adding the numbers from 0 to 4, and not to 5. This is because a "for" loop always starts counting from 0 (unless otherwise), and always stops 1 before the end of the range.

```
DEBUG: n=0 total=0
DEBUG: n=1 total=1
DEBUG: n=2 total=3
DEBUG: n=3 total=6
DEBUG: n=4 total=10
Sum of numbers 1 to 5 is 10
```

This is actually the sum of the numbers from 0 to 4, not 1 to 5

![](img/72d218a7a73c4d4abc7be582ebd85385_150_1.png)

# Fix the faulty line

The range should go from 1 up to "top_num + 1", so that the loop adds up the numbers from 1 to "top_num" (5).

```python
top_num = 5
total = 0
for n in range(1, top_num + 1):
    total = total + n
    print('DEBUG: n=', n, 'total=', total)
    input(0)
print('Sum of numbers 1 to', top_num, 'is', total)
```

The new range will count from 1 and stop at "top_num" (1 less than "top_num+1")

# Correct output

The "print" command shows that the program is adding the numbers from 1 to 5 and getting the correct answer. The bug has now been fixed!

```
DEBUG: n=1 total=1
DEBUG: n=2 total=3
DEBUG: n=3 total=6
DEBUG: n=4 total=10
DEBUG: n=5 total=15
Sum of numbers 1 to 5 is 15
```

"n=3", the total is (1+2+3)

The correct answer is now printed

![](img/72d218a7a73c4d4abc7be582ebd85385_150_2.png)

![](img/72d218a7a73c4d4abc7be582ebd85385_150_3.png)

![](img/72d218a7a73c4d4abc7be582ebd85385_150_4.png)

# Algorithms

An algorithm is a set of instructions for performing a task. Some algorithms are more efficient than others and take less time or effort. Different types of algorithms can be used for simple tasks such as sorting a list of numbers.

> SEE ALSO
> 16–17 Think like a computer
> Libraries 152–153

# Insertion sort

Imagine you've been given your class's exam papers to put in order from the lowest to the highest mark. "Insertion sort" creates a sorted section at the top of the pile and then inserts each unsorted paper into the correct position.

- How it works: "Insertion sort" goes through each of these stages sorting the numbers far quicker than a human could.

When counting the positions, Python starts at 0

![](img/72d218a7a73c4d4abc7be582ebd85385_151_0.png)

- Sorting in order: "Insertion sort" takes each paper in turn and inserts it into the correct (sorted) place.

6 is sorted into position 1

6 is more than 2, so is sorted after 2 in the sorted section

5 is sorted into position 1

The value of 5 is between 2 and 6, and so moves to position 1. 6 shifts to position 2

1 is sorted into position 0

1 is less than 2, so moves to position 0. 2, 5 and 6 shuffle down

4 is sorted into position 2

4 is between 2 and 5, so moves to position 2. 5 and 6 shuffle down

3 is sorted into position 2

Sorted!

4, 5, and 6 shuffle along to make room for 3 in position 2

# Selection sort

"Selection sort" works differently to "insertion sort". It swaps pairs of items rather than constantly shifting all of the items. Each swap moves one number to its final (sorted) position.

Swap the smallest value with the first value

![](img/72d218a7a73c4d4abc7be582ebd85385_152_0.png)

Swapping positions: Switching one with another is usually quick and doesn't affect anything else in the list. Swaps 1 and 2

![](img/72d218a7a73c4d4abc7be582ebd85385_152_1.png)

Swap the smallest value in the unsorted part (2) with the first value in the unsorted part (6)

Swaps 2 and 6

![](img/72d218a7a73c4d4abc7be582ebd85385_152_2.png)

3 is the smallest value in the unsorted part. Swap it with 5, the first value in the unsorted part

Swaps 3 and 5

![](img/72d218a7a73c4d4abc7be582ebd85385_152_3.png)

5 isn't in the right position yet, but 4 is smaller so it's swapped

Swaps 4 and 6

![](img/72d218a7a73c4d4abc7be582ebd85385_152_4.png)

The largest number is in last position after the swap, so no further swapping is required

Sorted! ![](img/72d218a7a73c4d4abc7be582ebd85385_152_5.png)

# EXPERT TIPS

# Sorting in Python

There are lots of different sorting algorithms, each with different strengths and weaknesses. Python's "sort()" uses an algorithm called "Timsort", named after its designer, Tim Peters. It's based on two sorting algorithms: "Insertion sort" and "Merge sort". Type in this code to see how it works. "a" is a list of unsorted numbers

```python
>>> a = [4, 9, 3, 8, 2, 6, 5, 7]
>>> a.sort()
>>> a
[1, 2, 3, 4, 5, 6, 7, 9]
```

This calls the "sort()" function. The numbers in list "a" are now sorted

# Libraries

Writing new code takes time, so it's useful to reuse bits of other programs. These snippets of code can be shared in packages called “libraries”.

# Standard Library modules

Python comes with a “Standard Library” that has lots of useful bits of code ready to use. Stand-alone sections of a library called “modules” can be added to Python to make it even more powerful.

| SEE ALSO | |
| :--- | :--- |
| Making 154–155 | windows |
| Color and 156–157 | coordinates |

- Batteries included: Python's motto is "batteries included". This means it comes with lots of ready-use code.
- Random: This module can pick a random number, or shuffle a list into a random order.
- Turtle: This module is used to draw lines and shapes on the screen. ![](img/72d218a7a73c4d4abc7be582ebd85385_153_0.png) ![](img/72d218a7a73c4d4abc7be582ebd85385_153_1.png)
- Time: The Time module gives the current time and date, and can calculate dates—for instance, what will it be in three days' time?![](img/72d218a7a73c4d4abc7be582ebd85385_153_2.png)
- Tkinter: Tkinter is used to make buttons, windows, and other graphics that help users interact with programs.
- Math: Use the Math module to work with complex mathematical calculations.![](img/72d218a7a73c4d4abc7be582ebd85385_153_3.png)
- Socket: The code in this module helps connect to each other over networks and the Internet.![](img/72d218a7a73c4d4abc7be582ebd85385_153_4.png) ![](img/72d218a7a73c4d4abc7be582ebd85385_153_5.png)

# Importing modules

Before using a module, you have to tell the computer to import it so it can be used by your program. This allows the bits of code it contains to be available to you. Importing modules is done using the "import" command. Python can import modules in a few different ways.

> EXPERT TIPS

# Pygame

Pygame is a Python library designed for writing video games. Pygame gives you access to sound modules and special graphics that can be used in games. You'll be able to use Pygame once you have a good understanding of the basics of Python covered in this book.![](img/72d218a7a73c4d4abc7be582ebd85385_154_0.png)

```python
import random
```

This way of importing requires you to type the module name at the start of the code. It makes it easier to read which module it came from.

```python
import random
random.randint(1, 6)
random.choice(my_list)
```

The module name comes before each function

Imports all the functions from the Random Module

```python
from random import *
```

Importing a module like this works well for small programs. But it can get confusing with bigger programs because it's unclear which module the function belongs to.

```python
randint(1, 6)
choice(my_list)
```

This code doesn't show which module the function comes from

Imports only the "randint" function

```python
from random import randint
```

"from random randint"
You can import a single function from the module. This can be more efficient than importing the whole module if it's the only function you want to use.

```python
randint(1, 6)
```

Only the "randint" function is available

# Help and document

| Help |
| About IDLE |
| IDLE Help |
| Python Docs |

Not sure how to use a module or what functions are available? The Python Library Reference has all the details. Simply click on the library you want to learn more about. It's a good idea to get know the libraries, modules, and functions that are available, so you don't waste time writing code that already exists.

Help!
at the top of any IDLE window, click "Help" and choose "Python Docs". This brings up lots of useful information.
