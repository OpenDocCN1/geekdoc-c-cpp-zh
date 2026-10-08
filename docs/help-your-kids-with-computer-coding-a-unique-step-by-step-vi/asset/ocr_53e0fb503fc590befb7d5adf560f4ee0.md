# Dictionaries

Dictionaries are like lists but they have labels. These labels, called "keys", identify items instead of index numbers. Every item in a dictionary has a key and a value. Items in a dictionary don't have to stay in a particular order, and the contents of a dictionary can be changed.

+   - Create a dictionary: This program creates a dictionary called "age". The key for each item is the name of a person. The value is their age.

![](bbox=[0.715, 0.045, 0.937, 0.193])

Dictionaries use curly brackets

Items in a dictionary are separated by commas

Use a colon between a key and a value

```
>>> { 'Mary': 10, 'Sanjay': 8 }
```

A key works the same way as an index number

A value stored in the dictionary (always comes after a colon)

```
>>> print(age) {'Sanjay': 8, 'Mary': 10}
```

The key for this item is 'Sanjay'

The value of 'Mary' is 10

Name of the dictionary

Dictionary name

New key

+   - Print the dictionary: The order of the items can change, because the positions of items in dictionary are not fixed.

+   - Add a new item: A new value can be added to the dictionary by labeling it with the new key.

```
>>> age['Owen'] = 11
{'Owen': 11, 'Sanjay': 8, 'Mary': 10}
```

Adds a new item to the dictionary

The new value is now in the dictionary

The existing value are still there

```
>>> age['Owen'] = 12
>>> print(age)
{'Owen': 12, 'Sanjay': 8, 'Mary': 10}
```

Assign a new value to the item labeled 'Owen'

+   - Change a value: Assign a new value to an existing key to change its value.

The value for 'Owen' has changed

This deletes the item labeled

+   - Delete an item: An item in a dictionary doesn't affect other items because they are identified by their key, not by their position in the dictionary.

```
>>> del age['Owen']
>>> print(age)
Sanjay': 8, 'Mary': 10}
```

The item labeled 'Owen' no longer appears in the dictionary