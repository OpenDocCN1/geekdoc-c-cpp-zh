# STEP 5

This naturally means you can incorporate various functions into your own code, such as:

```
```python
time.strftime("%a")
time.strftime("%B")
time.strftime("%b")
time.strftime("%H")
time.strftime("%H%M")
```
```

![](bbox=[0.067, 0.241, 0.492, 0.386])

# STEP 8

You saw at the end of the previous section, in the code to calculate Pi to however many decimal places the users wanted, you can time a particular event in Python. Take the code from above and alter it slightly by including:

```
```python
start_time=time.time()
```
```

Then there's:

```
```python
endtime=time.time()-start_time
```
```

![](bbox=[0.509, 0.255, 0.935, 0.386])

# STEP 6

Note the last two entries, with %H and %H%M, as you can see these are the hours and minutes and as the last entry indicates, entering them as %H%M doesn’t display the time correctly in the Shell. You can easily rectify this with:

```
```python
time.strftime("%H:%M")
```
```

![](bbox=[0.067, 0.491, 0.492, 0.673])

# STEP 9

The output will look similar to the screenshot below. The timer function needs to be either side of the input statement, as that’s when the variable name is being created, depending on how long the user took to log in. The length of time is then displayed on the last line of the code as the endtime variable.

![](bbox=[0.509, 0.485, 0.935, 0.673])

# STEP 7

This means you’re going to be able to display either the current time or the time when something occurred, such as a user entering their name. Try this code in the Editor:

```
```python
import time
name=input("Enter login name: ")
print("Welcome", name, "%d")
print("User:", name, "logged in at", time.strftime("%H:%M"))
```
```

Try to extend it further to include day, month, year and so on.

![](bbox=[0.067, 0.864, 0.492, 0.971])

# STEP 10

There’s a lot that can be done with the time module; some of it is quite complex too, such as displaying the number of seconds since January 1st 1970. If you want to drill down further into the time module, then in the Shell enter: help(time) to display the current Python version help file for the time module.

![](bbox=[0.509, 0.837, 0.935, 0.971])