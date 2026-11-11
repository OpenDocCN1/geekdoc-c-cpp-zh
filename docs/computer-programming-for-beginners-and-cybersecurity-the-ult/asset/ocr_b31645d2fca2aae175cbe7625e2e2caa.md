```
['France', 'Spain', 'Switzerland']
```

```
In []: country_list.reverse ()
```

```
print (liste_pays)
```

```
['Switzerland', 'Spain', 'France', 'United States', 'India', 'China']
```

# The Comprehension Lists

These are lists built iteratively. They are often very useful because they are more efficient than using loops to build lists. Here is a simple example:

```
In []: list_init = [4,6,7,8]
```

```
list_comp = [val ** 2 for val in list_init if val% 2 == 0]
```

The list_comp list allows you to store the even elements of list_init set to the square.

We will have:

```
In []: print (list_comp)
```

```
[16,36,64]
```

This notion of comprehension list is very effective. It avoids useless code (loops on a list) and performs better than creating a list iteratively. It also exists in dictionaries but not on tuples that are unchangeable. We will be able to use comprehension lists in the framework of the manipulation of data tables.

# Strings—Character Lists

Strings in Python are encoded by default (since Python 3) in Unicode. You can declare a string of characters in three ways:

```
string1 = "Python for the data scientist"
```

```
string2 = 'Python for the data scientist'
```

```
string3 = """ "Python for the data scientist" """
```