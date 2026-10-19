# 9.2 List<T> Collection

# Examples

```
List<int> unitsSold = new List<int>();        // Creates a List of int type named unitsSold
List<string> movies = new List<string>();      // Creates a List of string type named movies
List<int[]> classGrades = new List<int[]>();   // Creates a List of int arrays named classGrades
List<Array> examScores = new List<Array>();    // Creates a List of arrays named examScores
List<Customer> customers = new List<Customer>(); // Creates a List of Customer type
```

Note that names like unitsSold and movies in the above examples are the names of variables that reference the List, although, for the sake of brevity, we describe them as the names of Lists.

In general, the term “List” is used in place of “variable that references the List object.”

# Adding Items to a List

The Add() method adds a specified item to the end of the List. When the number of items in a List exceeds its initial capacity, the capacity is doubled automatically.

# Examples Using the Lists Created Above

```
unitsSold.Add(205);        // adds 205 to the end of the unitsSold List
movies.Add("Pocahontas");
int[] studentGrades = {85,91,80};        // creates the array to be inserted into a List
classGrades.Add(studentGrades);          // Adds the array studentGrades to the List, classGrades
```

# Accessing an Item

One way to access each element is by specifying the index of the element.

# Examples

```
unitsSold[0] returns the int type number stored in the first element of unitsSold
classGrades[0] returns the array stored in the first element of classGrades
```

You also may use the foreach loop to access every element of the List.