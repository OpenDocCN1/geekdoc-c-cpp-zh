```
```
>>>d = 1
>>>print  `That is %d dead %s!` % (d, s) 
That is 1 dead parrot!
```
```

Python also has a string utility module for tools such as case conversion, converting strings to numbers, etc. Here’s yet another example:

**Listing 6.7: String utilities**

```
```
>>> import string #standard utilities module
>>> S = "spammmify" 
>>> string.upper(S)  #convert to uppercase 
'SPAMMIFY' 
>>> string.find(S, "mm")   #return index of substring 
3 
>>> string.atoi("42"), `42`  #convert from/to string 
(42, '42') 
>>> string.join(string.split(S, "mm"), "XX") 
'spaXXify'
```
```

Notice the example of the second to last line. Backquotes are used to convert an object into a string. This is one way around the "don’t mix strings and numbers" problem from earlier. I’ll leave the last line example above as a mental test. See if you can figure out what the statement is doing.

Though it’s not strictly a string operation (it can be used with just about anything that can be measured), the `len()` method can be used to give you the length of a string. For example,

**Listing 6.8: Finding the length of a string**

```
```
>>>string = "The Life of Brian" 
>>>print len(string) 
17 
>>>len("The Meaning of Life") 
19
```
```

As shown in the second example above, you don’t necessarily have to use a print statement (or `print()` function in Python 3.x) to display a value. Simply writing what you want will print out the result. However, this doesn’t always work in your favor. Sometimes the object