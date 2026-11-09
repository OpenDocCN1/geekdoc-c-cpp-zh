+   8. Select a number

Now use the randrange() function from the random module to select a random number from 0 to 100. Put this line at the bottom of your code.

```
```python
noun = random.choice(nouns)
number = random.randrange(0, 100)
```
```

# EXPERT TIPS

# Constants

A constant is a special type of variable whose contents can't be changed. The constant string.punctuation holds a string of characters used for punctuation. To see what it holds, type import string into the shell, followed by print(string.punctuation).

```
```python
>>> import string
>>> print(string.punctuation)
!"#$%&'()*+,-./:;<=>?@[\]^_`{|}~
```
```

Characters in this constant

+   9. Select a special character

Using the random.choice() function again, add this line to pick a random punctuation character. This will make your password even harder to crack!

```
```python
number = random.randrange(0, 100)
special_char = random.choice(string.punctuation)
```
```

This is a constant.

+   10. Create the new secure password

It's time to assemble all the different parts to create the new secure password. Type these two lines of code at the end of your program.

Your secure password will be stored in this variable.

This changes the random number into a string.

```
```python
password = adjective + noun + str(number) + special_char
print('Your new password is: %s' % password)
```
```

This displays the new password in the shell.

# EXPERT TIPS

# Strings and integers

The str() function turns a whole number (an integer) into a string. If you don't use this function, Python shows an error when you try to add an integer to a string. Test it: type print('route ' +66) into the shell window.

```
```python
>>> print('route ' +66)
Traceback (most recent call last):
  File "<pyshell#0>", line 1, in <module>
    print('route ' +66)
TypeError: Can't convert 'int' object to str implicitly
```
```

Error message

To avoid this error, use the str() function to change the number into a string first.

```
```python
>>> print('route ' +str(66))
route 66
```
```

The number goes inside the brackets of the str() function.