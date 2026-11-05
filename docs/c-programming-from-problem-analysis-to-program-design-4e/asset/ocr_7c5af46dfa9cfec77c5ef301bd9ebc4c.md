# BitArray

The BitArray class stores a collection of bit values. These bit values are represented as Booleans, where true indicates that the bit is on and false indicates the bit is off. There are several ways to create and initialize BitArrays. Example 8-17 illustrates some of the ways.

# EXAMPLE 8.17

```
// Creates and initializes several BitArrays
BitArray firstBitArr = new BitArray(10);
BitArray secondBitArr = new BitArray(10, true);
bool[] boolArray = new bool[5] {true, false, true, true, false};
BitArray thirdBitArr = new BitArray(boolArray);
```

There are a number of constructors available with this collection. As shown in the first line in Example 8-17, you can send an integer representing the number of elements. These elements are initially all set to false. The second line sets the values to true when the secondBitArr is created. Another option is to use an array of Booleans to set the values. The thirdBitArr has a mixture of true and false values. This is also illustrated in Example 8-17. The BitArray class has both Count and Length properties. Both retrieve the number of elements in the array. Length can also be used to set the number of elements thus enabling BitArrays to grow or shrink in size dynamically. An Item property is available for setting the actual value. BitArray has member methods of Set( ) and SetAll( ), which can be used to change the value of elements. Example 8-18 illustrates accessing elements from the array.

# EXAMPLE 8.18

```
// Sets all the elements to true
firstBitArr.SetAll(true);

// Sets the first element to false
firstBitArr[0] = false;

// Sets the last index to false.
secondBitArr.Set(myBA.Count - 1, false);

// Gets the value of the last element
Console.WriteLine(thirdBitArr.Get(myBA.Count - 1));
```

BitArrays are most commonly used to represent a simple group of Boolean flags and are especially useful for working with large data sets. They compactly store individual bits or Boolean values. As shown in Example 8-18, there are several ways to access the elements