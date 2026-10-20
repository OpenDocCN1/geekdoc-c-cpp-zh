# STEP 5

For example, use the divide by zero error. You can create an exception where the code can handle the error without Python quitting due to the problem:

```
try:
    a=int(input("Enter the first number: "))
    b=int(input("Enter the second number:"))
    print(a/b)
except ZeroDivisionError:
    print("You have tried to divide by zero!")
else:
    print("You didn’t divide by zero. Well done!")
```

![](bbox=[0.065, 0.293, 0.49, 0.382])

# STEP 6

You can use exceptions to handle a variety of useful tasks. Using an example from our previous tutorials, let’s assume you want to open a file and write to it:

```
try:
    txt = open("/home/pi/Documents/textfile.txt", "r")
    txt.write("This is a test. Normal service will shortly resume!")
except IOError:
    print ("Error: unable to write the file. Check permissions")
else:
    print ("Content written to file successfully. Have a nice day.")
    txt.close()
```

![](bbox=[0.065, 0.608, 0.49, 0.665])

# STEP 7

Obviously this won’t work due to the file textfile.txt being opened as read only (the "r" part). So in this case rather than Python telling you that you’re doing something wrong, you’ve created an exception using the IOError class informing the user that the permissions are incorrect.

![](bbox=[0.065, 0.767, 0.485, 0.938])

# STEP 8

Naturally, you can quickly fix the issue by changing the "r" read only instance with a "w" for write. This, as you already know, will create the file and write the content then commit the changes to the file. The end result will report a different set of circumstances, in this case, a successful execution of the code.

![](bbox=[0.51, 0.21, 0.935, 0.382])

# STEP 9

You can also use a finally: block, which works in a similar fashion but you can’t use else with it. To use our example from Step 6:

```
try:
    txt = open("/home/pi/Documents/textfile.txt", "r")
    try:
        txt.write("This is a test. Normal service will shortly resume!")
    finally:
        print ("Content written to file successfully. Have a nice day.")
        txt.close()
except IOError:
    print ("Error: unable to write the file. Check permissions")
```

![](bbox=[0.51, 0.618, 0.935, 0.665])

# STEP 10

As before an error will occur as you’ve used the "r" read-only permission. If you change it to a "w", then the code will execute without the error being displayed in the IDLE Shell. Needless to say, it can be a tricky getting the exception code right the first time. Practise though, and you will get the hang of it.

![](bbox=[0.51, 0.767, 0.935, 0.938])