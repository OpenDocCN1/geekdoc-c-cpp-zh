
```python
print('\n')

# clear list values
even_nums.clear()
print("Even number list after clearing is: ", even_nums)
print('\n')

# extend the empty list
even_nums.extend(['Tom', 1, 'python'])
print("Even number list after extending is: ", even_nums)
print('\n')

# insert new element at index 0
even_nums.insert(0, 'new')
print("Even number list after inserting at index 0 is: ", even_nums)
print('\n')

# pop list last element
even_nums.pop()
print("Even number list after popping is: ", even_nums)
print('\n')

# find the index of 'Tom' and change it to Nick
index_python = even_nums.index('Tom')
even_nums[index_python] = 'Nick'

print("Even number after replacing Tom is: ", even_nums)
```

**Output:**

Length of even_nums list is: 6

Even numbers are:
0
2
4
6
8
10

Even numbers less than 5 are: [0, 2, 4]

Even number list after appending is: [0, 2, 4, 6, 8, 10, 12]

12 occurs 1 times in even_nums list

Even number list after clearing is: []

Even number list after extending is: ['Tom', 1, 'python']

Even number list after inserting at index 0 is: ['new', 'Tom', 1, 'python']

Even number list after popping is: ['new', 'Tom', 1]

Even number after replacing Tom is: ['new', 'Nick', 1]

## Tuples

Tuples are similar to lists as they also store a collection of items. In fact, tuples can be considered immutable lists. Tuples are immutable; once assigned, they can’t change. This makes them more efficient and faster. Tuples are defined using parentheses, whereas lists are defined using square brackets. To create a tuple, put comma-separated values in parentheses.

```python
my_tuple = (1,3,5)
```

For a single-value tuple, follow the value with a comma. Without a comma, Python considers it a number.

```python
my_tuple = (1,)
```

In this snippet, we create tuples and try to modify their values; however, Python throws a type error because tuples are immutable.

```python
# create a tuple

# single value tuple
tu1 = (1, )

print("Single value tuple: ", tu1)
# Multi values tuple
tu2 = (1, 'a', 'python')
print("Multi value tuple: ", tu2)
print("tuple type is ", type(tu2))

# try modifying tuple
tu2[2] = 'C++'
```

```text
Single value tuple:  (1,)
Multi value tuple: (1, 'a', 'python')
tuple type is  <class 'tuple'>

--------------------------------------------
Traceback (most recent call last):
  File "<ipython-input-7-a5d65c274c9b>", line 13, in <module>
    11
    12 # try modifying tuple
---> 13 tu2[2] = 'C++'

TypeError: 'tuple' object does not support item assignment
```

### Tuples methods

Similar to lists, tuples support basic methods like indexing, `len`, slicing, and the `in` membership operator. Tuples also support the `index` and `count` methods. Note that tuples don’t have as many methods as lists because they are immutable.

### Example 2: *Tuple methods*

In this example, we perform basic methods on a tuple. Note that these methods are the same as in list methods.

```python
# Basic tuple methods
tu = ('Tom', 'Jane', 'Python', 10, 'Tom')

# len()
print("Tuple length is :", len(tu))

# Element access
print("Last element of tuple is :",tu[-1])

# slicing
print("tu[0:3] is :",tu[0:3])

# index method
print("'Python' is at index:",tu.index('Python'))

# count method
print("'Tom' occurs:",tu.count('Tom'))
```

```text
Tuple length is : 5
Last element of tuple is : Tom
tu[0:3] is : ('Tom', 'Jane', 'Python')
'Python' is at index: 2
'Tom' occurs: 2
```

## Dictionaries

Dictionaries are key-value pairs. While lists and tuples are accessed by a position index, dictionary values are accessed by their corresponding key. The keys must be immutable, such as strings, numbers, or even tuples, but not lists because lists are mutable. Keys are also unique; you can't have 2 values with the same key.

Dictionaries are defined by comma-separated key: value pairs in curly brackets.

To create an empty dictionary:

```python
my_dict = {}
```

or

```python
my_dict = dict()
```

To create a basic dictionary:

```python
num_dict = {'one':1, 'two':2, 'three':3}
```

### Basic dictionary methods

To access a dictionary value, use its key.

```python
num_dict = {'one':1, 'two':2, 'three':3}
num_dict['one'] is 1
```

Membership is similar to tuples and lists except that it checks for keys.

```python
num_dict = {'one':1, 'two':2, 'three':3}
'one' in num_dict returns True
```

To add a new key-value pair, use the assignment operator.

```python
num_dict = {'one':1, 'two':2, 'three':3}
num_dict['four'] = 4
num_dict now is {'one':1, 'two':2, 'three':3, 'four':4}
```

- `dict.clear` – clears the dictionary.

    ```python
    num_dict = {'one':1, 'two':2, 'three':3}
    num_dict.clear()
    num_dict now is {}
    ```

- `dict.get(key)` – retrieves a dictionary value by a key and returns None if no such key exists.

    ```python
    num_dict = {'one':1, 'two':2, 'three':3}
    num_dict.get('one') returns 1
    ```

- `dict.pop(key)` – removes key:value pair corresponding to key.

    ```python
    num_dict = {'one':1, 'two':2, 'three':3}
    num_dict.pop('three') removes 3
    num_dict now is {'one':1, 'two':2}
    ```

- `dict.items()` – returns a list of (key, value) tuples.

    ```python
    num_dict = {'one':1, 'two':2, 'three':3}
    num_dict.items() returns [('one', 1), ('two', 2), ('three', 3)]
    ```

- `dict.keys()` – returns a dict_keys object containing all dictionary keys.

    ```python
    num_dict = {'one':1, 'two':2, 'three':3}
    num_dict.keys() returns dict_keys(['one', 'two', 'three'])
    ```

- `dict.values()` – returns a list of dictionary values.

    ```python
    num_dict = {'one':1, 'two':2, 'three':3}
    num_dict.values() returns [1, 2, 3]
    ```

### Example 3: *Dictionary methods*

In Example 3, we use and experiment with the dictionary methods we learned.

```python
# create a dictionary of shopping items quantity
shopcart = {'chips':2, 'ink cartridge':1, 'paper':1}

# dictionary length counts key-value pairs
print('Shopcart is:', shopcart)
print('Your shopcart distinct items are ', len(shopcart))
print('\n')

# shop cart include a pens ?
pens_in = 'pens' in shopcart

# membership test
print("There is a pen in shopping cart?", pens_in)
print('\n')

# accessing a value
print("The number of chips items is", shopcart['chips'])
print('\n')

# add a pair
shopcart['orange juice'] = 4
print(shopcart)
print('\n')

# get method
print("Quantity of orange juice is", shopcart.get('orange juice'))
print('\n')

# pop method removes element at a key
shopcart.pop('paper')
print(shopcart)
print('\n')

# get items, keys, values
items = shopcart.items()
keys = shopcart.keys()
values = shopcart.values()

print("Shopcart items are:", items)
print("Shopcart keys are:", keys)
print("Shopcart values are:", values)
```

```text
Shopcart is: {'chips': 2, 'ink cartridge': 1, 'paper': 1}
Your shopcart distinct items are 3

There is a pen in shopping cart False

The number of chips items is 2

{'chips': 2, 'ink cartridge': 1, 'paper': 1, 'orange juice': 4}

Quantity of orange juice is 4

{'chips': 2, 'ink cartridge': 1, 'orange juice': 4}

Shopcart items are: dict_items([('chips', 2), ('ink cartridge', 1), ('orange juice', 4)])
Shopcart keys are: dict_keys(['chips', 'ink cartridge', 'orange juice'])
Shopcart values are: dict_values([2, 1, 4])
```

### Example 4 – Guess World Capitals

In this example, we use both a list and a dictionary. A dictionary `capital_dict` is used to make country:capital key pairs. Then we get the dictionary keys using the `keys()` method and store them in the `countries` list. This is essential so we can use the `random.choice()` function, which takes a list and returns a value from the list randomly. Then inside an infinite `while` loop, the user is asked for a capital using the `input` function and the answer is compared to the actual capitals.

```python
# World capital game
import random

# World capitals dictionary
capital_dict={
    'spain':'madrid',
    'france':'paris',
    'germany':'berlin',
    'norway':'oslo',
    'india':'new delhi',
    'egypt':'cairo'
}

# get countries and convert them to a list so we can use random function
countries = list(capital_dict.keys())
print ("Let's learn World Capitals. Enter quit to quit the game.")

while True:
    # pick a random country
    country = random.choice(countries)
    capital = capital_dict[country]

    guess = input(f'What is the capital of {country}.')
    # if user types quit, quit
    if guess.lower() == "quit":
        break
    elif guess.lower() == capital:
        print(f'Correct !')
        break
    else:
        print(f'Incorrect. The capital of {country} is {capital}.')
```
