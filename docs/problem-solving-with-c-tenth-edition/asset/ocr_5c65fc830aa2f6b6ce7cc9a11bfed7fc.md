# PROGRAMMING EXAMPLE

# A Class for a Partially Filled Array

Display 11.10 shows the definition for a class called TemperatureList, whose objects are lists of temperatures. You might use an object of type TemperatureList in a program that does weather analysis. The list of temperatures is kept in the member variable list, which is an array. Since this array will typically be only partially filled, a second member variable, called size, is used to keep track of how much of the array is used. The value of size is the number of indexed variables of the array list that are being used to store values.

An object of type TemperatureList is declared like an object of any other type. For example, the following declares myData to be an object of type TemperatureList:

```
TemperatureList myData;
```

This declaration calls the default constructor with the new object myData, and so the object myData is initialized so that the member variable size has the value 0, indicating an empty list.

Once you have declared an object such as myData, you can add an item to the list of temperatures (that is, to the member array list) with a call to the member function addTemperature as follows:

```
myData.addTemperature(77);
```

In fact, this is the only way you can add a temperature to the list myData, since the array list is a private member variable. Notice that when you add an item with a call to the member function addTemperature, the function call first tests to see if the array list is full and adds the value only if the array is not full.

The class TemperatureList is very specialized. The only things you can do with an object of the class TemperatureList are to initialize the list so it is empty, add items to the list, check if the list is full, and output the list. To output the temperatures stored in the object myData (declared previously), the call would be as follows:

```
cout << myData;
```

With the class TemperatureList you cannot delete a temperature from the list (array) of temperatures. You can, however, erase the entire list and start over with an empty list by calling the default constructor, as follows:

```
myData = TemperatureList();
```

The type TemperatureList uses almost no properties of temperatures. You could define a similar class for lists of pressures or lists of distances or lists of any other data expressed as values of type double. To save yourself the trouble of defining all these different classes, you could define a single class that represents an arbitrary list of values of type double without specifying what the values represent.