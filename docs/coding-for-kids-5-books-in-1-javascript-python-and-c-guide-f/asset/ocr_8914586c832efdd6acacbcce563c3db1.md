```
```
>>> True and True
True
>>> True and False
False
>>> False and False
False
>>> False and True
False
>>> True or True
True
>>> True or False
True
>>> False or True
True
>>> False or False
False
>>> not True
False
>>> not False
True
```
```

# # elif keyword

While only one of the if or else code blocks will execute, you may have a case where you want one of many code blocks to execute based on the condition. You can use the elif keyword for such a case. The elif keyword is roughly translated to “else if”.

```
```python
number = int(input("Number? "))

if number > 10:
    print("{} is greater than 10".format(number))
elif number > 5:
    print("{} is greater than 5".format(number))
else:
    print("{} is not greater than 5 or 10".format(number))
```
```

The above code is similar to the ‘number-checker’ code we had earlier, but now it also checks if the number is greater than 5. Below is the output when the user inputs 8

```
```
Number? 8
8 is greater than 5
>>> |
```
```