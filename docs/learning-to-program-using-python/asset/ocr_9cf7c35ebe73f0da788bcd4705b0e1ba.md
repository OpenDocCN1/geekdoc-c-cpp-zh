and process each line. You could also use it to process command- line arguments by "filtering" out the program name. Again, here's an example:

# Listing 6.5: String slicing

```
```python
>>> S = "spam"
>>> S[1:3], S[1:], S[:-1]    # slicing: extract section
('pa', 'pam', 'spa')
```
```

You'll notice that the colon symbol is used when slicing. The colon acts as a separator between the upper and lower index values. If one of those values is not given, Python interprets that to mean that you want everything from the index value to the end of the string. In the example above, the first slice is from index 1 (the second letter, inclusive) to index 3 (the 4th letter, exclusive). You can consider the index to actually be the space before each letter; that's why the letter “m” isn't included in the first slice but the letter “p” is.

The second slice is from index 1 (the second letter) to the end of the string. The third slice starts at the end of the string and goes backwards.

# ## 6.3 String Formatting

Formatting strings is simply a way of presenting the information on the screen in a way that conveys the information best. Some examples of formatting are creating column headers, dynamically creating a sentence from a list or stored variable, or stripping extraneous information from the strings, such as excess spaces. (Python 3.x has a new way of formatting strings; this will be discussed in the 19 section below.)

Python supports the creation of dynamic strings. What this means is that you can create a variable containing a value of some type (such as a string or number) then "call" that value into your string. You can process a string the same way as in C if you choose to, such as %d for integers and %f for floating point numbers. Here's an example:

# Listing 6.6: Dynamic string creation

```
```python
>>> S = "parrot"
```
```