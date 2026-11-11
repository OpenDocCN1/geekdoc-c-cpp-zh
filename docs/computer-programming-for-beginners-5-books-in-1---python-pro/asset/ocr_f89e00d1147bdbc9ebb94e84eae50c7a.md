condition, however you don’t want it to act in any way. This is when you should use the “pass” keyword instead. What it does is essentially form a null statement. This means that the program will know to skip this loop and move on to the next block of code. Here’s an example:

```
while True:
    my_input = int (new_input (“$? : >> “))
    if my_input > 0:
        pass
    else:
        print (“This input is negative”)
```

Now let’s see an example of using break and continue:

```
offset = 0
total = 0
while True:
    my_input = float (input (“$? : >> “))
    if my_input < 0:
        if offset == 0:
            print (“You need to enter some values!”)
            continue
        break
    total += my_input
    offset += 1
    print (offset, ‘:’, total)
```

It’s worth mentioning that in Python you can nest multiple loops, as well as conditional statements. In fact, you can have an infinite structure of loop levels, however it’s not recommended to go to that extreme. Nesting too many loops can