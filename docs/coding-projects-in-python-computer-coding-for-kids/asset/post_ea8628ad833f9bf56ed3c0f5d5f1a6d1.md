
## max()

The max() function selects the maximum value from the parameters you give it. Hit the enter/return key to see the value on the screen. This function takes multiple parameters, which must be separated by commas.

```python
>>> max(10, 16, 30, 21, 25, 28)
30
```

The maximum value is the highest number in the brackets.

Always separate multiple parameters with commas.

## min()

The function min() does the opposite of max(). It selects the minimum value from the parameters you put inside its brackets. Experiment for yourself with the max() and min() functions.

```python
>>> min(10, 16, 30, 21, 25, 28)
10
```

When you hit the enter/return key, the code shows you the lowest number.

## Another way of calling

Some of the different types of data we’ve come across so far, such as integers, strings, and lists, have their own functions. These functions must be called in a special way. You type the data or the name of the variable holding the data, followed by a dot, the function’s name, and finally brackets. Test out these code snippets in the shell.

![](img/6b18a113f7aa9338e32f3ac1fa217987_46_0.png)

Don't forget the dot.

```python
>>> 'bang'.upper()
'BANG'
```

This is the new string, all in capitals.

Empty brackets mean that no parameters are needed.

## upper()

The upper() function takes an existing string and returns a new string in which all the lower-case characters are changed to upper-case (capitals).

## replace()

The function has two parameters. Two parameters are needed for this function: the first is the part of a string you want to replace, while the second is the string you want to put in its place. The function returns a new string with the replacement made.

```python
>>> message = 'Python makes me happy'
>>> message.replace('happy', ':D')
'Python makes me :D'
```

The new string replaces happy with :D.

## reverse()

Use this function when you want to reverse the order of the items in a list. Here, it’s used to reverse a list of numbers stored in the variable countdown. Instead of printing the list as [1, 2, 3], the function makes it print [3, 2, 1].

The list of numbers stored in the variable countdown:

```python
>>> countdown = [1, 2, 3]
>>> countdown.reverse()
>>> print(countdown)
[3, 2, 1]
```

The list is now reversed.

## Making a function

The best functions have a clear purpose and a good name that explains what they do—think of the `check_guess()` function you used in Animal Quiz. Follow these instructions to create, or “define,” a function that calculates the number of seconds in a day and then prints the answer on the screen.

### 1 Define the function

Create a new file in IDLE. Save it as “functions.py”. Type these lines into the editor window. An indent is added at the start of each line in the function. Save the file again, then run the code to see what happens.

The name of the function

There are no parameters yet.

```python
def print_seconds_per_day():
    hours = 24
    minutes = hours * 60
    seconds = minutes * 60
    print(seconds)

print_seconds_per_day()
```

Variables

The line prints the value of the variable seconds.

The keyword `def` tells Python that this block of code is a function.

The lines after the name must be indented 4 spaces, to show Python that they are part of the function.

This command calls the function.

86400

The number of seconds in a day appears in the shell.

### 2 Add parameters

If you want to give your function any values to work with, you put them inside the brackets as parameters. For example, to find out the total number of seconds in a particular number of days, change your code to look like this. The function now has a parameter `days`. You can specify the number of days when you call the function. Try it out yourself.

```python
def print_seconds_per_day(days):
    hours = days * 24
    minutes = hours * 60
    seconds = minutes * 60
    print(seconds)

print_seconds_per_day(7)
```

The function’s parameter

This line uses the parameter `days`.

Gives a value (7) to the parameter days

Existing lines of code are shown in grey and new lines of code in bold.

604800

The number of seconds in 7 days.

### EXPERT TIPS

**Top advice**

It’s important to define your functions before you use them in your main code. When you’re learning to code with Python, it’s helpful to put your functions at the top of your file, after any import statements. By doing this, you won’t make the mistake of trying to call a function before you’ve defined it.

![](img/6b18a113f7aa9338e32f3ac1fa217987_47_0.png)

### 3. Return a value

Once you have a function that does something useful, you'll want to use the results from that function in the rest of your code. You can get values out of a function by "returning" them. Change your code as shown here to get the return value from your function. You should rename the function to match its new purpose. Don't try to run the code just yet.

```python
def convert_days_to_seconds(days):
    hours = days * 24
    minutes = hours * 60
    seconds = minutes * 60
    return seconds
```

The function's new name

The keyword `return` gives the value of the variable `seconds`.

The line that called the function is deleted, as the function now has a new name and purpose.

### 4. Store and use the return value

You can store the return value from a function in a variable to use later in your code. Add this code under your function. It stores the return value and uses it to calculate the number of milliseconds (thousandths of a second). Try it out and experiment with the number of days.

```python
def convert_days_to_seconds(days):
    hours = days * 24
    minutes = hours * 60
    seconds = minutes * 60
    return seconds

total_seconds = convert_days_to_seconds(7)
milliseconds = total_seconds * 1000
print(milliseconds)
```

This calls the function and gives a value (7) to the parameter `days`.

The return value is stored in the variable `total_seconds`.

604800000

This line prints the value of `milliseconds`.

The total number of seconds is converted into milliseconds and stored in the variable `milliseconds`.

This is the number of milliseconds in 7 days.

### EXPERT TIPS

### Naming your functions

In Step 3, you changed the name of your function from `print_seconds_per_day()` to `convert_days_to_seconds()`. Just like with variables, it's important that the name you use accurately explains what the function does. This makes your code much easier to understand.

The rules for naming functions are similar to those for variables. Function names can contain letters, numbers, and underscores, but they should begin with a letter. If there are several words in the name, the words should be separated by underscores.

## Fixing bugs

If something’s wrong with your code, Python will try to help by showing an error message. These messages can seem a bit puzzling at first, but they’ll give you clues about why your program isn’t working and how to fix it.

### Error messages

Both the IDLE editor and the shell window can show error messages if mistakes are detected. An error message tells you what type of error has occurred and where to look in your code.

### Messages in the shell

Python displays error messages in red text in the shell window. The program stops working when an error message appears. The message tells you which line of code caused the error to happen.

This pop-up box tells you there’s a syntax error, which means there’s a typing mistake.

### Messages in the IDLE editor

A pop-up box warns you there’s an error. Click OK to return to your program. There will be a red highlight on or near the error.

![](img/6b18a113f7aa9338e32f3ac1fa217987_49_0.png)

```text
>>>
Traceback (most recent call last):
    File "Users/Craig/Developments/top-secret-python-book/age.py", line 21, in <module>
        print('I am'+ age + 'years old')
TypeError: Can't convert 'int' object to str implicitly
```

This line tells you it’s a type error (see page 50).

The error is on line 21.

![](img/6b18a113f7aa9338e32f3ac1fa217987_49_1.png)

### EXPERT TIPS — Finding bugs

When an error message appears in the shell, right-click it and choose “Go to file/line” on the drop-down menu. The IDLE editor jumps straight to that line of code so you can start debugging.

![](img/6b18a113f7aa9338e32f3ac1fa217987_49_2.png)
