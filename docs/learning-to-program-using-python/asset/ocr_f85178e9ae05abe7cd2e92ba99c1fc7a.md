+   4. They are mutable but can't be modified like lists or strings; they are the only data type that supports mapping.
5. Internally, dictionaries are implemented as a hash table.

Here's the (now standard) list of common operations:

+   - d1 = {} Empty dictionary
- d2 = {'spam': 2, 'eggs': 3} Two-item dictionary
- d3 = {'food': {'ham': 1, 'egg': 2}} Nesting
- d2['eggs'], d3['food']['ham'] Indexing by key
- d2.has_key('eggs'), d2.keys(), d2.values() Methods: membership test, keys list, values list, etc.
- len(d1) Length (number stored entries)
- d2[key] = new, del d2[key] Adding/changing, deleting

# ## 8.1 Making a dictionary

As previously stated, you create dictionaries and access items via a key. The key can be of any immutable type, like a string, number, or tuple. The values can be any type of object, including other dictionaries. The format for making a dictionary is shown in Listing 8.1:

```
Listing 8.1: Dictionary format

```python
>>> dictionary = {"key_name": "value"}
```
```

However, the key name and value can be anything allowed, such as:

```
Listing 8.2: Dictionary keys example

```python
>>> dictionary = {"cow":"barn", 1:"pig", 2:["spam", "green", "corn"]}
```
```

Notice that the brackets for dictionaries are curly braces, the separator between a key word and it's associated value is a colon, and that each key/value is separated by a comma. This is just some of the things that can cause syntax errors in your program.