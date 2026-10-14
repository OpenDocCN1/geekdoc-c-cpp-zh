but for now just be aware that they are what you use to step through a range of values. As you can see they can be used for strings or, more often, numbers.

The second example is simply a comparison. Does the letter “k” exist in the value stored by “myjob”? If yes, then Python will return a numeric value of 1, indicating yes. If “k” didn’t exist, it would return a 0. This particular case is most often used in word processing applications, though you can probably think of other situations where it would be useful.

# ## 6.2  Indexing and slicing strings

Strings in Python are handled similar to arrays in C. Unlike C arrays, characters within a string can be accessed both front and backwards. Front-ways, a string starts of with a position of 0 and the character desired is found via an offset value (how far to move from the end of the string). However, you also can find this character by using a negative offset value from the end of the string. I won’t go deeply into it, but here’s a quick example:

```
Listing 6.4: String indexing  
```python
>>> S = "spam"
>>> S[0], S[-2] # indexing from the front and rear
('s', 'a')
```
```

Indexing is simply telling Python where a character can be found within the string. Like many other languages, Python starts counting at 0 instead of 1. So the first character’s index is 0, the second character’s index is 1, and so on. It’s the same counting backwards through the string, except that the last letter’s index is -1 instead of 0 (since 0 is already taken). Therefore, to index the final letter you would use -1, the second to the last letter is -2, etc. Knowing the index of a character is important for slicing.

Slicing a string is basically what it sounds like: by giving upper and lower index values, we can pull out just the characters we want. A great example of this is when processing an input file where each line is terminated with a newline character; just slice off the last character