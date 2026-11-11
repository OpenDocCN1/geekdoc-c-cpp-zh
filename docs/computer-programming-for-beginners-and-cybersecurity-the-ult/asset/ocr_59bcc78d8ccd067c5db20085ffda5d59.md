.remove (val): remove the first occurrence of the value val from the list

# Extract an Item from a List

As we have seen above, it is possible to extract an element using the brackets:

```
list1 [0]
```

We are often interested in the extraction of several elements. It is done by using the two points:

```
list1 [0: 2] or list1 [: 2]
```

In this example, we see that this system extracts two elements: the indexed element in 0 and the one indexed in position 1. So we have as a rule that i: j goes from the element i included in element j not included. Here are some other examples:

```
# Extract the last element
```

```
list1 [-1]
```

```
Extract the last 3 elements  list1 [-3: -1] or list1 [-3:]
```

# A concrete example

Suppose we wanted to create a list of countries. These countries are ordered in the list according to their population. We will try to extract the first three and the last three.

```
In []: country_list = ["China,” “India,” “United States,” “France,” "Spain,” “Swiss”]
```

```
In []: print (country_list [: 3])
```

```
['China', 'India', 'United States']
```

```
In []: print (country_list[-3:])
```