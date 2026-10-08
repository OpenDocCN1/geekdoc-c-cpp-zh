# 8.7 Passing Arrays and Array Elements to Methods

| Ace of Hearts | Ten of Hearts | Deuce Hearts | Deuce of Clubs |
|--- | --- | --- | --- |
| Jack of Hearts | Nine of Spades | Four of Hearts | Seven of Clubs |
| Queen of Spades | Seven of Diamonds | Five of Diamonds | Ace of Hearts |
| Four of Clubs | Ten of Diamonds | Jack of Clubs | Six of Diamonds |
| Eight of Diamonds | King of Hearts | Three of Clubs | King of Spades |
| King of Hearts | Six of Diamonds | Deuce of Spades | Five of Spades |
| Queen of Clubs | King of Clubs | Queen of Hearts | Seven of Hearts |
| Ace of Diamonds | Deuce of Hearts | Four of Diamonds | Nine of Clubs |
| Queen of Diamonds | Jack of Diamonds | Six of Hearts | Nine of Diamonds |
| Nine of Hearts | Three of Hearts | Six of Clubs | Eight of Hearts |

**Fig. 8.12** Card-shuffling-and-dealing.app (Part 2 of 2.)

# 8.7 Passing Arrays and Array Elements to Methods

To pass an argument to a method, specify the name of the array without any brackets. For example, if hourlyTemperatures is declared as

```
var hourlyTemperatures = new double[24];
```

then the method call

```
modifyArray(hourlyTemperatures);
```

passes the reference of array hourlyTemperatures to modifyArray. Every array object "knows" its own length (and makes it available via its Length property). Thus, when we pass an array object to a method, we do not pass the array length as an additional argument.

# Specifying an Array Parameter

For a method to receive an array reference through a method call, the method must list an array parameter. For example, the method header for method modifyArray might be written as

```
void modifyArray(double[] b)
```

indicating that modifyArray receives the reference of an array of doubles in parameter b. The method passes array hourlyTemperatures reference, so when the method calls variable b, it refers to the same array object as hourlyTemperatures in the calling method.

# Pass-By-Value vs. Pass-By-Reference

When an argument is an entire array or an individual array element of a reference type, the called method receives a copy of the reference. However, when an argument to a method is an individual array element of value type, the called method receives a copy of the element's value. To pass an individual array element to a method, use the indexed name of the array as an argument (e.g., hourlyTemperatures[2]). If you want to pass a value-type array element to a method, you must use the ref keyword as shown in Section 7.18.

# Passing an Entire Array vs. Passing a Single Array Element

Figure 8.13 demonstrates the difference between passing an entire array and passing a value-type array element to a method. The foreach statement at lines 16–19 outputs the five