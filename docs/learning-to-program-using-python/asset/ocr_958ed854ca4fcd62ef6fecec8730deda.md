The sequences within a tuple are essentially protected from modification. This way, you won't accidentally change the values, nor can someone misuse an API to modify the data. (An API is an application programming interface. It allows programmers to use a program without having to know the details of the whole program.)

Tuples can be used as keys for dictionaries. Honestly, I don't think I've ever used this, nor can I think of a time when you would need to. But it's there if you ever need to use it.

Tuples are used in string formatting, by holding multiple values to be inserted into a string. In case you don't remember, here's a quick example:

```
Listing 9.1: String formatting with tuples

```
>>>val1 = "integer"
>>>val2 = 2
>>>"The %s value is equal to %d" % (val1, val2)
'The integer value is equal to 2'
```
```

# 9.2 Sequence Unpacking

So, to create a tuple, we treat it like a list (just remembering to change the brackets).

```
Listing 9.2: Packing a tuple

```
>>>tuple = (1, 2, 3, 4)
```
```

The term for this is packing a tuple, because the data is “packed into” the tuple, all wrapped up and ready to go. So, to remove items from a tuple you simply unpack it.

```
Listing 9.3: Unpacking a tuple

```
>>>first, second, third, fourth = tuple
>>> first
1
>>> second
```
```