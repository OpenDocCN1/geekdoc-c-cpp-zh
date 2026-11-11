Now, let’s reverse the order of the original list with the help of the “reverse” method:

```
reversed (character_inventory)
```

```
<listreverseiterator object at 0x81abf0c>
```

```
character_inventory.reverse()
```

```
character_inventory
```

```
[‘spell scroll’, ‘staff’, ‘healing herb’, ‘bag of gold’]
```

Take note that when we change sequences with certain methods and functions we sometimes don’t get a new sequence in response, but instead we return an object. For instance, in our example we have an iterator object. This is used in “for” loops as if it were a sequence. As a result, when we used the “reversed” function we obtained a reversed iterator object. Here’s how it works:

```
for element in reversed(character_inventory):
```

```
print item
```

```
spell scroll
staff
healing herb
bag of gold
```

# Enter the Matrix

No, not the movie, but the multidimensional lists! This is a fancy way of saying that we can nest lists inside other lists, thus forming a matrix or a multidimensional list. This way we can use lists to hold data in the form of a table. Here’s an example of nested lists assigned to a variable:

```
my_matrix = [[11, 12, 13], [21, 22, 23], [31, 32, 33]]
```

This is a three by three matrix. If you remember your elementary school math classes it may look familiar.

When you iterate through a list you should probably use the “for” loop as it is considered a standard practice. Why? Because if you aren’t sure how many