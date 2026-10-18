Enter name: Raja
Number: 3333

The program first creates **phone map** interactively with three names and then inserts two more names into the map. Then, it displays all the names and their telephone numbers available in the map. Now the program requests the user to enter the name of a person. The program looks into the map, using the person name as a key, for the associated number and then prints the number.

> > **NOTE:** *That the names are printed in alphabetical order, although the original data was not. The list is automatically sorted using the key. In our example, the key is the name of person.*

We can access the two parts of an entry using the members **first** and **second** with an iterator of the **map** as illustrated in the program. That is,

```
(*p).first
```

gives the key, and

```
(*p).second
```

gives the value.

# 14.7  Function Objects

A function object is a function that has been wrapped in a class so that it looks like an object. The class has only one member function, the overloaded ( ) operator and no data. The class is templa-tized so that it can be used with different data types.

Function objects are often used as arguments to certain containers and algorithms. For example, the statement