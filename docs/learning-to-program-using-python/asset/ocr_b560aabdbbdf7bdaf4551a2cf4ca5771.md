```
[0, 1, 2, 3, 4]
>>> range(2, 5) #start at 2 and end at 5 (remember
 the index values)
[2, 3, 4]
>>> range(0, 10, 2) #start at 0, end at 10 (index
 value), with an increment of 2
[0, 2, 4, 6, 8]
```

As you can see, a single argument gives you a list of integers, starting from 0 and ending at one less than the argument (because of the index). Two arguments give a starting number and the max value while three arguments adds a stepping value, i.e. how many numbers to skip between each value.

Counter loops simply count the number of times the loop has been processed. At the end of the loop, a variable is incremented to show that the loop has been completed. Once a certain number of loops have occurred, the loop is executed and the rest of the program is executed.

# ### 11.7 pass Statement

The pass statement is simply a way to tell Python to continue moving, nothing to see here. Most often, the pass statement is used while initially writing a program. You may create a reference to a function but haven't actually implemented any code for it yet. However, Python will be looking for something within that function. Without having something to process, the Python interpreter will give an exception and stop when it doesn't find anything. If you simply put a pass statement in the function, it will continue on without stopping.

Listing 11.12: pass statements

```
```python
if variable > 12:
    print "Yeah, that's a big number."
else: pass
```
```