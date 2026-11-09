# ### 3. Return a value

Once you have a function that does something useful, you'll want to use the results from that function in the rest of your code. You can get values out of a function by "returning" them. Change your code as shown here to get the return value from your function. You should rename the function to match its new purpose. Don't try to run the code just yet.

```
```python
def convert_days_to_seconds(days):
    hours = days * 24
    minutes = hours * 60
    seconds = minutes * 60
    return seconds
```
```

The function's new name

The keyword `return` gives the value of the variable `seconds`.

The line that called the function is deleted, as the function now has a new name and purpose.

# ### 4. Store and use the return value

You can store the return value from a function in a variable to use later in your code. Add this code under your function. It stores the return value and uses it to calculate the number of milliseconds (thousandths of a second). Try it out and experiment with the number of days.

```
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
```

This calls the function and gives a value (7) to the parameter `days`.

The return value is stored in the variable `total_seconds`.

604800000

This line prints the value of `milliseconds`.

The total number of seconds is converted into milliseconds and stored in the variable `milliseconds`.

This is the number of milliseconds in 7 days.

**EXPERT TIPS**

# ### Naming your functions

In Step 3, you changed the name of your function from `print_seconds_per_day()` to `convert_days_to_seconds()`. Just like with variables, it's important that the name you use accurately explains what the function does. This makes your code much easier to understand.

The rules for naming functions are similar to those for variables. Function names can contain letters, numbers, and underscores, but they should begin with a letter. If there are several words in the name, the words should be separated by underscores.