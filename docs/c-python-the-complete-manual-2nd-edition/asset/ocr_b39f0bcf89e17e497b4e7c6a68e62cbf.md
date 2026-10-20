# Writing to Files

The ability to read external files within Python is certainly handy but writing to a file is better still. Using the write() function, you’re able to output the results of a program to a file, that you can then read() back into Python.

# WRITE AND CLOSE

The write() function is slightly more complex than read(). Along with the filename you must also include an access mode which determines whether the file in question is in read or write mode.

# STEP 1

Start by opening IDLE and enter the following:

```
t=open("/home/pi/Documents/text.txt","w")
```

Change the destination from /home/pi/Documents to your own system. This code will create a text file called text.txt in write mode using the variable ‘t’. If there’s no file of that name in the location, it will create one. If one already exits, it will overwrite it, so be careful.

![](bbox=[0.06, 0.48, 0.49, 0.62])

# STEP 3

However, the actual text file is still blank (you can check by opening it up). This is because you’ve written the line of text to the file object but not committed it to the file itself. Part of the write() function is that you need to commit the changes to the file; you can do this by entering:

```
t.close()
```

![](bbox=[0.51, 0.45, 0.93, 0.62])

# STEP 2

You can now write to the text file using the write() function. This works opposite to read(), writing lines instead of reading them. Try this:

```
t.write("You awake in a small, square room. A single table stands to one side, there is a locked door in front of you.")
```

Note the 109. It’s the number of characters you’ve entered.

![](bbox=[0.06, 0.78, 0.49, 0.92])

# STEP 4

If you now open the text file with a text editor, you can see that the line you created has been written to the file. This gives us the foundation for some interesting possibilities: perhaps the creation of your own log file or even the beginning of an adventure game.

![](bbox=[0.51, 0.74, 0.93, 0.92])