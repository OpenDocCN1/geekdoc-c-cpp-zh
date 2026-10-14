```
class IndirectlyDerivedFromType ( DerivedFromBuiltInType ) :
	pass
```

# # 15.6 A Note About Style

As mentioned previously, Python has a certain “style-syntax” that is considered the “right” way to write Python programs. PEP 8 is the document that describes all of the “approved” ways of writing. One of these is how to identify classes, functions, methods, etc.

Classes should be written with the first letter capitalized; any additional words in the class name should also be capitalized: class SpamAndEggs(object). Functions and methods should be written in lower-case, with each word separated by underscores: def bunny_vicious_bite(). Constants (variables that don't change value) should be written in all upper case: MAX_VALUE = 22.

There are many other stylistic ideas to be concerned about. I'll admit, I'm not the best about following Python's stylistic conventions but I try to follow them as best I can remember. Even if I don't follow “the Python way”, I do try to be consistent within my own programs. My personal suggestion is to read PEP 8 and look at the source code for different Python programs, then pick a style that works best for you. The most important thing is to have a consistent style.