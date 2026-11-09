# Syntax errors

When you get a syntax error message, it’s a hint that you’ve typed something incorrectly. Perhaps your fingers slipped and hit a wrong letter? Don’t worry—these are the easiest errors to fix. Check through your code carefully and try to spot what went wrong.

The closing bracket is missing—it needs another curved bracket here.

```
input('What is your name?')
```

The first quotation mark is missing. It needs to be a single quote to match.

```
print(It is your turn')
```

This is a spelling mistake—it should be short_shots.

```
total_score = (long_shots * 3) + (short_shots * 2)
```

# ▷ Things to look out for

Are you missing a bracket or quotation mark? Do your pairs of brackets and quotation marks match? Have you made a spelling mistake? All these things can cause syntax errors.

# Indentation errors

Python uses indentation to understand where blocks of code start and stop. An indentation error means something is wrong with the way you’ve structured the code. Remember: if a line of code ends with a colon (:), the next line must be indented. Press the space bar four times to manually indent a line.

# ▽ Indent each new block

In your Python programs, you’ll often have one block of code within another block, such as a loop that sits inside a function. Every line in a particular block must be indented by the same amount. Although Python helps by automatically indenting after colons, you still need to check that each block is indented correctly.

```
if weekday == True:
print('Go to school')
```

This line of code would trigger an indentation error message.

```
if weekday == True:
    print('Go to school')
```

Four spaces

You need to indent the code on the second line like this to fix the error.

![](bbox=[0.536, 0.63, 0.933, 0.975])