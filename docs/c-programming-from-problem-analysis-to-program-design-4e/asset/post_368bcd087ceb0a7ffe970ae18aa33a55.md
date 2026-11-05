
## TABLE 8-2 Members of the string class (continued)

| Methods and properties | Description | Example |
| --- | --- | --- |
| PadRight( ) | Overloaded. Left-aligns the characters in the `string`, padding on the right with spaces or a specified character. | `s = sValue.PadRight(20, '#');`<br>`Console.WriteLine(s);`<br><br>`//Displays`<br>`C# Programming#########` |
| Remove( ) | Deletes a specified number of characters beginning at a specified position. | `s = sValue.Remove(3, 8);`<br>`Console.WriteLine(s);`<br><br>`//Displays`<br>`C# ing` |
| Replace( ) | Overloaded. Replaces all occurrences of a character or `string` with another character or string. | `s = sValue.Replace("gram", "GRAM");`<br>`Console.WriteLine(s);`<br><br>`//Displays`<br>`C# ProGRAMming` |
| Split( ) | Overloaded. Identifies the substrings in the `string` that are delimited by one or more characters specified in an array, then places the substrings into a `string` array. | `string[] sn = sValue.Split(' ');`<br>`foreach (string i in sn)`<br>`    Console.WriteLine(i);`<br><br>`//Displays`<br>`C#`<br>`Programming` |
| StartsWith( ) | Determines whether the beginning of the `string` matches the specified `string`. | `Console.WriteLine(`<br>`    sValue.StartsWith("C#"));`<br><br>`//Displays`<br>`True` |
| Substring( ) | Overloaded. Retrieves a substring from the `string`. | `Console.WriteLine(sValue.Substring(3, 7));`<br>`//Displays`<br>`Program` |
| ToCharArray( ) | Copies the characters in the `string` to a character array. | `char[] cArray = sValue.ToCharArray(0, 2);`<br>`Console.WriteLine(cArray);`<br>`//Displays`<br>`C#` |
| ToLower( ) | Overloaded. Returns a copy of the `string` in lowercase. | `Console.WriteLine(sValue.ToLower());`<br>`//Displays`<br>`c# programming` |
| ToString( ) | Overloaded. Converts the value of the instance to a `string`. | `int x = 234;`<br>`s = x.ToString();`<br>`Console.WriteLine(s);`<br>`//Displays`<br>`234` |
| ToUpper( ) | Overloaded. Returns a copy of the `string` in uppercase. | `Console.WriteLine(sValue.ToUpper());`<br>`//Displays`<br>`C# PROGRAMMING` |
| Trim( )<br>TrimEnd( )<br>TrimStart( ) | Overloaded. Removes all occurrences of a set of specified characters from the beginning and end. | `s = sValue.Trim('g','i','n','m','C');`<br>`Console.WriteLine(s);`<br>`//Displays`<br>`#Progra` |

**NOTE** Notice that the methods identified as class methods in the second column, such as `Compare`, `Concat`, and `Copy`, prefix the name of the method in the call with the `string` data type (e.g. `s = string.Copy(sValue)`).

Most string member arguments that take a string object accept a string literal. C# has two types of string literals. You have used one of them, the quoted literal. Quoted string literals appear between double quotation marks (" ") and are the most common type found in languages. The other type, @-quoted string literals, start with the at symbol (@) and are also enclosed in double quotation marks. The @-quoted string literals are referred to as the verbatim string literal because the characters between the double quotes are interpreted verbatim. There are two differences between the quoted and @-quoted string literal. With the @-quoted literal, escape sequence characters, such as `'\t'` and `'\n'`, are not recognized as special characters. The second difference is that the @-quoted literal enables you to use a keyword for an identifier. This is illustrated in Example 8-16.

**EXAMPLE 8-16**

Using the @-quoted literal with the statement here displays the `'\t'` as part of the output:

```csharp
Console.WriteLine(@"hello \t world");
//Displays
hello \t world
```

Without the @-quoted literal, a tab is inserted:

```csharp
Console.WriteLine("hello \t world");
//Displays
hello    world
```

Tables 8-1 and 8-2 included a number of the extremely useful methods and properties of the ArrayList and String classes. Other members exist. Do not reinvent the wheel and write code for functions that already exist. These members have been tried and tested. The key to using the members is to experiment and play with them. The C# online documentation with Visual Studio includes many examples that you will want to explore.

## Other Collection Classes

Collection classes are classes that enable you to store and retrieve various groups of objects. As you just experienced with arrays, when you have data that is closely related, it is more efficient to group the data together under a common name. This enables you to write code to process all elements in the collection instead of writing code to handle each individual object. There are a number of other collection classes, in addition to ones already introduced, that can be used in C#. You saw that an ArrayList offered the advantage of being able to dynamically increase in size as new objects were added. The .NET framework also includes classes for storing bit values. There are predefined classes for creating stacks, queues, and hash tables. As with the ArrayList class, in order to instantiate objects of these other collection classes, you need to include a `using System.Collections;` to the list of namespaces. In the section that follows, some of these collection classes are explored.

### BitArray

The BitArray class stores a collection of bit values. These bit values are represented as Booleans, where true indicates that the bit is on and false indicates the bit is off. There are several ways to create and initialize BitArrays. Example 8-17 illustrates some of the ways.

**EXAMPLE 8-17**

```csharp
// Creates and initializes several BitArrays
BitArray firstBitArr = new BitArray(10);
BitArray secondBitArr = new BitArray(10, true);
bool[] boolArray = new bool[5] {true, false, true, true, false};
BitArray thirdBitArr = new BitArray(boolArray);
```

There are a number of constructors available with this collection. As shown in the first line in Example 8-17, you can send an integer representing the number of elements. These elements are initially all set to false. The second line sets the values to true when the secondBitArr is created. Another option is to use an array of Booleans to set the values. The thirdBitArr has a mixture of true and false values. This is also illustrated in Example 8-17. The BitArray class has both Count and Length properties. Both retrieve the number of elements in the array. Length can also be used to set the number of elements thus enabling BitArrays to grow or shrink in size dynamically. An Item property is available for setting the actual value. BitArray has member methods of `Set( )` and `SetAll( )`, which can be used to change the value of elements. Example 8-18 illustrates accessing elements from the array.

**EXAMPLE 8-18**

```csharp
// Sets all the elements to true
firstBitArr.SetAll(true);

// Sets the first element to false
firstBitArr[0] = false;

// Sets the last index to false.
secondBitArr.Set(secondBitArr.Count - 1, false);

// Gets the value of the last element
Console.WriteLine(thirdBitArr.Get(thirdBitArr.Count - 1));
```

BitArrays are most commonly used to represent a simple group of Boolean flags and are especially useful for working with large data sets. They compactly store individual bits or Boolean values. As shown in Example 8-18, there are several ways to access the elements in the array. There are a number of bitwise operations including OR, AND, XOR, and NOT that can be performed on elements in the array. Surveys or questionnaires that accept responses such as yes/no or true/false are good candidates for using a BitArray collection. Data can be stored as Booleans and then a loop could be used to process the results.

### Hashtable

**Hashing** is a technique used for a lot of applications in computer science. One use of hashing is to provide security when data is transmitted across networks. A message is encrypted following some type of algorithm, sent across a network, and then on the other end the same algorithm is used to decrypt or convert the message back to a readable form. This concept is often used in the field of cryptography (i.e., information security) with passwords. Passwords are hashed after the user enters them, then sent to a server and compared against the stored hash values there. This prevents the password from being intercepted in plain text.

Another application of hashing is used with large collections of data. Here instead of encrypting the full record or a password, the key or unique entry associated with the record is hashed or converted into an index and then the record is stored at that index location. Faster retrieval of individual elements or records is afforded using this principle. Instead of having to sequentially compare one record after another to determine if that is the record you want to process, the computer can now use the same algorithm that was used to store the record and go directly to the indexed location. The algorithm used to store the data is called a hash function. The hash function produces a hash code.

.NET includes a specialized collection class called a Hashtable that represents a collection of key/value pairs that are organized based on the hash code of the key. The hash code is just a number generated using a key with the objective of providing efficient insertion and find operations. There is no requirement that the data be in any specific order. One of the overriding goals is to design an algorithm that provides as few collisions as possible. Collisions occur when the algorithm that's used to create the hash code maps more than one record to the same index position. A good hash function tries to avoid collisions and tends to spread keys evenly in the array. Devising an effective algorithm is said to be an art and sometimes involves some trial and error before an effective algorithm is designed.

The mod operator (%) is often used with hashing algorithms. Often the key is not in numeric form and requires that a conversion occurs so that arithmetic can be performed. The eventual goal is to map the record to an index location in an array. For example, a hash function algorithm might take the Unicode representation for each character in the string and add each of those values. Once a sum is calculated, then the mod operator might be used. That summation could be divided by the first prime number larger than the number of data elements. The result of the mod operation might be the index where the record is stored.

You do not have to create your own algorithm when you use the .NET Hashtable class. A hash function is used to return a numeric hash code based on a key. The key, of course, is the value of some property of the object being stored. When an object is added
