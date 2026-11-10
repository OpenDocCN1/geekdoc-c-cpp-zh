
## Lists

When you want to store a lot of data, or perhaps the order of the data is important, you may need to use a list. A list can hold many items together and keep them in order. Python gives each item a number that shows its position in the list. You can change the items in the list at any time.

![](img/1bd24ab186f69fb18194b4174ca15178_26_0.png)

### 1 Multiple variables

Imagine you're writing a multiplayer game and want to store the names of the players in each team. You could create a variable for each player, which might look like this...

```python
>>> rockets_player_1 = 'Rory'
>>> rockets_player_2 = 'Rav'
>>> rockets_player_3 = 'Rachel'
>>> planets_player_1 = 'Peter'
>>> planets_player_2 = 'Pablo'
>>> planets_player_3 = 'Polly'
```

With three players per team, you'd need six variables.

### 2 Put a list in a variable

...but what if there were six players per team? Managing and updating so many variables would be difficult. It would be better to use a list. To create a list, you surround the items you want to store with square brackets. Try out these lists in the shell.

```python
>>> rockets_players = ['Rory', 'Rav',
'Rachel', 'Renata', 'Ryan', 'Ruby']
>>> planets_players = ['Peter', 'Pablo',
'Polly', 'Penny', 'Paula', 'Patrick']
```

The list items must be separated by commas.

This list is stored in the variable planets_players.

### 3 Getting items from a list

Once your data is in a list, it's easy to work with. To get an item out of a list, first type the name of the list. Then add the item's position in the list, putting it inside square brackets. Be careful: Python starts counting list items from 0 rather than 1. Now try getting different players' names out of your team lists. The first player is at position 0, while the last player is at position 5.

```python
>>> rockets_players[0]
'Rory'
>>> planets_players[5]
'Patrick'
```

This line gets the first item in the list, from position 0.

This line gets the last item in the list, from position 5.

Hit enter/return to retrieve the item.

## Pineapples and zebras

Let’s try an example using the shell. We can represent having five pineapples and two zebras by using the variables `pineapples` and `zebras`. Type these lines into the shell.

```python
>>> pineapples = 5
>>> zebras = 2
```

This variable stores the number of pineapples.

This variable stores the number of zebras.

![](img/1bd24ab186f69fb18194b4174ca15178_28_0.png)

### Make comparisons

Now try typing the following lines of code to compare the values of the two variables. After you’ve typed each line, press the return key and Python will tell you if the statements are True or False.

The number of pineapples is greater than the number of zebras.

```python
>>> pineapples > zebras
True
```

```python
>>> zebras < pineapples
True
```

The number of zebras is less than the number of pineapples.

The number of pineapples and the number of zebras aren’t equal.

```python
>>> pineapples != zebras
True
```

**LINGO**

### Boolean expressions

Statements about variables and values that use the logical operators always give us a Boolean value, such as True or False. Because of this, these statements are called Boolean expressions. All of our statements about pineapples and zebras are Boolean expressions.

Variable

Logical operator

```python
>>> pineapples != zebras
True
```

Boolean value

Variable

### Multiple comparisons

You can use `and` and `or` to combine more than one comparison. If you use `and`, both parts of the comparison must be correct for the statement to be True. If you use `or`, only one part needs to be correct.

```python
>>> (pineapples == 3) and (zebras == 2)
False
```

One part (pineapples == 3) is incorrect, so the statement is False.

```python
>>> (pineapples == 3) or (zebras == 2)
True
```

One part is correct (zebras == 2), so the statement is True.

## Ride the rollercoaster

A sign at the theme park says you must be over 8 years old and taller than 1.4 metres to ride the rollercoaster. Mia is 10 years old and 1.5 metres tall. Let's use the shell to check whether she can go for a ride. Type the following lines of code to create variables for Mia's age and height and assign the correct values to them. Type the rules for going on the rollercoaster as a Boolean expression, then hit the enter/return key.

![](img/1bd24ab186f69fb18194b4174ca15178_29_0.png)

These two lines assign values to the variables.

```python
>>> age = 10
>>> height = 1.5
>>> (age > 8) and (height > 1.4)
True
```

This is a Boolean expression meaning 'older than 8 and more than 1.4 metres tall'.

Mia can go on the rollercoaster!

### Branching

Computers often need to make decisions about which parts of a program to run. This is because most programs are designed to do different things in different situations. The route through the program splits like a path branching off into side paths, each leading to a different place.

![](img/1bd24ab186f69fb18194b4174ca15178_29_1.png)

**LINGO**

### Condition

A condition is a Boolean expression (a True-or-False comparison) that helps a computer decide which route to take when it reaches a branch in the code.

#### School or park?

Imagine you have to decide what route to walk each day based on the answer to the question 'Is today a weekday?' If it's a weekday, you take the route to school; if it's not, you take the route to the park. In Python, the different routes through a program lead to different blocks of code. A block can be one statement or several, all indented by four spaces. The computer uses a test called a condition to figure out which blocks it should run next.

![](img/1bd24ab186f69fb18194b4174ca15178_29_2.png)

#### One branch

The simplest branching command is an `if` statement. It only has one branch, which the computer takes if the condition is True. This program asks the user to say if it’s dark outside. If it is, the program pretends that the computer is going to sleep! If it’s not dark, `is_dark == 'y'` is False, so the “Goodnight!” message isn’t displayed.

This line asks the user to reply “y” (yes) or “n” (no).

```python
is_dark = input('Is it dark outside? y/n')

if is_dark == 'y':
    print('Goodnight! Zzzzzzzzzzzzz....')
```

Condition

This branch is taken if the condition is true.

The code shows this message in the shell window.

#### Two branches

Do you want a program to do one thing if a condition’s True and another thing if it’s False? If so, you need a command with two branches, called an `if-else` statement. This program asks if the user has tentacles. If they answer “Yes”, it decides they must be an octopus! If they answer “No”, it decides they’re human. Each decision prints a different message.

This line asks for input from the user.

Condition

```python
tentacles = input('Do you have tentacles? (y/n)')
if tentacles == 'y':
    print('I never knew octopuses could type!')
else:
    print('Greetings, human!')
```

This block runs if the condition is True.

This block runs if the condition is False.

#### Multiple branches

When there are more than two possible paths, the statement `elif` (short for “else-if”) comes in handy. This program asks the user to type in the weather forecast: either “rain”, “snow”, or “sun”. It then chooses one of three branches and weather conditions.

```python
weather = input('What is the forecast for today? (rain/snow/sun)')

if weather == 'rain':
    print('Remember your umbrella!')
elif weather == 'snow':
    print('Remember your woolly gloves!')
else:
    print('Remember your sunglasses!')
```

First condition

This block runs if the first condition is True.

Second condition

This block runs if the second condition is True.

This block runs if both conditions are false.

![](img/1bd24ab186f69fb18194b4174ca15178_30_0.png)

#### How it works

An `elif` statement must always come after `if` and before `else`. In this code, `elif` checks for snow only when the condition set by the `if` statement is False. You could insert additional `elif` statements to check for more types of weather.
