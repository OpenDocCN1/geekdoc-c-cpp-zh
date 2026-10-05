# Chapter 8 How to work with arrays and collections

# The syntax for retrieving a value from an array list

(type) arrayName[index]

# Code that creates an array list that holds decimal values

```
decimal[] salesTotals = {3275.68m, 4398.55m, 5289.75m, 1933.98m};
ArrayList salesTotals = new ArrayList();
foreach (decimal d in salesTotals)
salesTotals.Add(d);
```

# Another way to create the array list

```
ArrayList salesTotals = new ArrayList
{ 3275.68m, 4398.55m, 5289.75m, 1933.98m };
```

# Code that retrieves the first value from the array list

```
decimal sales1 = (decimal) salesTotals[0]; // sales1 = 3275.68
```

# Code that inserts and removes an element from the array list

```
salesTotals.Insert(0, 2745.73); // insert a new element
sales1 = (decimal) salesTotals[0]; // sales1 = 2745.73
deimal sales2 = (decimal) salesTotals[1]; // sales2 = 3275.68
sales2.RemoveAt(1); // remove the second element
sales2 = (decimal) salesTotals[1]; // sales2 = 4398.55
```

# Code that displays the array list in a message box

```
string salesTotalsString = "";
foreach (decimal d in salesTotals)
salesTotalsString += d + "\n";nMessageBox.Show(salesTotalsString, "Sales Totals");
```

![](bbox=[0.066, 0.558, 0.335, 0.673])

# Code that checks for an element in the array list and removes it if it exists

```
decimal x = 2745.73;
if (salesTotals.Contains(x))
salesTotals.Remove(x);
```

# Code that sorts and searches the array list

```
salesTotals.Sort();
int sales2Index = salesTotals.BinarySearch(sales2);
```

# Description

+   - The ArrayList class is part of the System.Collections namespace.
- The ArrayList class has the same properties and methods as the List<T> class in the System.Collections.Generic namespace. As a result, it's easy to convert code that uses the ArrayList class to use the List<T> class and vice versa.

Figure 8-17 How to work with an array list