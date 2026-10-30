operator< be defined for the type indexType. Of course, if the operator is not originally defined, you can define it. However the definition should have the usual properties expected of a comparison operator, i.e. it should be transitive and asymmetric.

Let us take a simple example. Suppose we want to store the population of different countries. Then we can create a map named Population, which will store the population value (numeric). Say we store the population in billions as a unit, so our valueType is double. We would like to use the name of the country to access the element corresponding to each country, so our indexType could be string. So we can define our map as follows.

```
map<string,double> Population;
```

Next we insert the information we want into the map, i.e. we specify the population of different countries.

```
Population["India"] = 1.21; // population of India is 1.21 billion
Population["China"] = 1.35;
Population["Unites States"] = 0.31;
Population["Indonesia"] = 0.24;
Population["Brazil"] = 0.19;
```

The first line, for example, creates an element whose value is 1.21, and whose index is "India". You use an array access like syntax also to refer to the created elements. For example, the following

```
cout << Population["Indonesia"] << endl;
```

will print 0.24, which is the value stored in the element whose index is "Indonesia".

You have to realize that while the statements look like array accesses superficially, their implementation will of course be very different. Effectively, what gets stored when you write Population["India"] = 1.21; is the pair ("India",1.21). The name Population really refers to a collection of such pairs. Subsequently, when we write Population["India"] we are effectively saying: refer to the second element of the pair whose first element is "India". So some code will have to execute to find this element (Section 20.5.2). So a lot is happening behind the scenes when you use maps.

What if you write two assignments for the same index, e.g.

```
Population["India"] = 1.21;
Population["India"] = 1.22;
```

This will have the effect you expect: the element created the first time around will be modified so that the value stored in it will change from 1.21 to 1.22.

An important operation you might want to perform on a map is to check if the map contains an element with a given index. Suppose you have read in the name of a country into a string variable country. Say you want to print out the population of that country if it is present in the map; else you want to print out a message saying that the population of that country is not known to the program. You can write this as follows