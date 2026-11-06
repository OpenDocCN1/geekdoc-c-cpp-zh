# # Random Module

The random module is one you will likely come across many times in your Python programming lifetime; as the name suggests, it’s designed to create random numbers or letters. However, it’s not exactly random but it will suffice for most needs.

# ## RANDOM NUMBERS

There are numerous functions within the random module, which when applied can create some interesting and very useful Python programs.

**STEP 1**  
Just as with other modules you need to import random before you can use any of the functions we’re going to look at in this tutorial. Let’s begin by simply printing a random number from 1 to 5:

```
```python
import random
print(random.randint(0,5))
```
```

![](bbox=[0.067, 0.514, 0.495, 0.628])

**STEP 2**  
In our example the number four was returned. However, enter the print function a few more times and it will display different integer values from the set of numbers given, zero to five. The overall effect, although pseudo-random, is adequate for the average programmer to utilise in their code.

![](bbox=[0.297, 0.646, 0.495, 0.794])

**STEP 3**  
For a bigger set of numbers, including floating point values, you can extend the range by using the multiplication sign:

```
```python
import random
print(random.random() *100)
```
```

Will display a floating point number between 0 and 100, to the tune of around fifteen decimal points.

![](bbox=[0.067, 0.988, 0.495, 1.0])

**STEP 4**  
However, the random module isn’t used exclusively for numbers. You can use it to select an entry from a list from random, and the list can contain anything:

```
```python
import random
random.choice([“Conan”, “Valeria”, “Belit”])
```
```

This will display one of the names of our adventurers at random, which is a great addition to a text adventure game.

![](bbox=[0.509, 0.586, 0.936, 0.742])

**STEP 5**  
You can extend the previous example somewhat by having random.choice() select from a list of mixed variables. For instance:

```
```python
import random
lst=[“David”, 44, “BDM Publications”, 3245.23, “Pi”, True, 3.14, “Python”]
rnd=random.choice(lst)
print(rnd)
```
```

![](bbox=[0.509, 0.917, 0.936, 0.992])