# STEP 5

To expand this code, you can reopen the file using `a`, for access or append mode. This will add any text at the end of the original line instead of wiping the file and creating a new one. For example:

```
```python
t=open("/home/pi/Documents/text.txt","a")
t.write("\n")
t.write("You stand and survey your surroundings. On top of the table is some meat, and a cup of water.\n")
```
```

![](bbox=[0.066, 0.282, 0.492, 0.407])

# STEP 8

You can pass variables to a file that you’ve created in Python. Perhaps you want the value of Pi to be written to a file. You can call Pi from the math module, create a new file and pass the output of Pi into the new file:

```
```python
import math
print("Value of Pi is: ",math.pi)
print("\nWriting to a file now...")
```
```

![](bbox=[0.509, 0.255, 0.935, 0.407])

# STEP 6

You can keep extending the text line by line, ending each with a new line (`\n`). When you’re done, finish the code with `t.close()` and open the file in a text editor to see the results:

```
```python
t.write("The door is made of solid oak with iron strips. It’s bolted from the outside, locking you in. You are a prisoner!\n")
t.close()
```
```

![](bbox=[0.066, 0.559, 0.492, 0.707])

# STEP 9

Now let’s create a variable called pi and assign it the value of Pi:

```
```python
pi=math.pi
```
```

You also need to create a new file in which to write Pi to:

```
```python
t=open("/home/pi/Documents/pi.txt","w")
```
```

Remember to change your file location to your own particular system setup.

![](bbox=[0.509, 0.565, 0.935, 0.707])

# STEP 7

There are various types of file access to consider using the `open()` function. Each depends on how the file is accessed and even the position of the cursor. For example, `r+` opens a file in read and write and places the cursor at the start of the file.

![](bbox=[0.066, 0.806, 0.492, 0.925])

# STEP 10

To finish, you can use string formatting to call the variable and write it to the file, then commit the changes and close the file:

```
```python
t.write("Value of Pi is: {}".format(pi))
t.close()
```
```

You can see from the results that you’re able to pass any variable to a file.

![](bbox=[0.509, 0.862, 0.935, 0.925])