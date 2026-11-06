# STEP 5

The opposite of the .split function is .join, where you will have separate items in a string and can join them all together to form a word or just a combination of items, depending on the program you’re writing. For instance:

```
alphabet="".join(["a","b","c","d","e"])
alphabet
```

This will display ‘abcde’ in the Shell.

![](bbox=[0.067, 0.245, 0.491, 0.385])

# STEP 8

As with the .split function, the separator doesn’t have to be a space, it can also be a comma, a full stop, a hyphen or whatever you like:

```
colours=["Red", "Green", "Blue"]
col=", ".join(colours)
col
```

![](bbox=[0.509, 0.227, 0.934, 0.385])

# STEP 6

You can therefore apply join to the separated name you made in Step 4, combining the letters again to form the name:

```
name="".join(name)
name
```

We’ve joined the string back together, and retained the list called name, passing it through the .join function.

![](bbox=[0.067, 0.518, 0.491, 0.665])

# STEP 9

There’s some interesting functions you apply to a string, such as .capitalize and .title. For example:

```
title="conan the cimmerian"
title.capitalize()
title.title()
```

![](bbox=[0.509, 0.485, 0.934, 0.665])

# STEP 7

A good example of using the join function is when you have a list of words you want to combine into a sentence:

```
list=["Conan", "raised", "his", "mighty", "sword", "and", "struck", "the", "demon"]
text=" ".join(list)
text
```

Note the space between the quotes before the .join function (where there were no spaces in the Step 6’s join)

![](bbox=[0.067, 0.829, 0.491, 0.956])

# STEP 10

You can also use logic operators on strings, with the ‘in’ and ‘not in’ functions. These enable you to check if a string contains (or does not contain) a sequence of characters:

```
message="Have a nice day"
"nice" in message

"bad" not in message
"day" not in message
"night" in message
```

![](bbox=[0.509, 0.829, 0.934, 0.956])