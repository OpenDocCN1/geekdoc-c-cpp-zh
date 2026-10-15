Fortunately, there are ways to limit the amount of boxing that occurs when using collections. One method that works well is to create a class based on the value type you need to work with. This might seem counterintuitive at first because it costs more to create a class. The key is how often you reuse the data contained in the class. By repeatedly using the object to interact with other objects, you avoid creating a temporary boxed object.

Examples in two important areas will help illustrate boxing. The first involves the use of arrays. When an array is created, the portion of the class that tracks the element of the array is created as a reference object, but each element of the array is created directly. Thus, an array of integers consists of an Array object and a set of Integer value types. When you update one of the values with another integer value, no boxing is involved:

```
Dim arrInt(20) as Integer
Dim intMyValue as Integer = 1

arrInt(0) = 0
arrInt(1) = intMyValue
```

Neither of these assignments of an integer value into the integer array that was defined previously requires boxing. In each case, the array object identifies which value on the stack needs to be referenced, and the value is assigned to that value type. The point here is that just because you have referenced an object doesn’t mean you are going to box a value. The boxing occurs only when the values being assigned are being transitioned from value types to reference types:

```
Dim strBldr as New System.Text.StringBuilder()
Dim mySortedList as New System.Collections.SortedList()
Dim count as Integer
For count = 1 to 100
    strBldr.Append(count)
    mySortedList.Add(count, count)
Next
```

The preceding snippet illustrates two separate calls to object interfaces. One call requires boxing of the value intCount, while the other does not. Nothing in the code indicates which call is which, but the Append method of StringBuilder has been overridden to include a version that accepts an integer, while the Add method of the SortedList collection expects two objects. Although the integer values can be recognized by the system as objects, doing so requires the runtime library to box these values so that they can be added to the sorted list.

When looking for boxing, the concern isn’t that you are working with objects as part of an action, but that you are passing a value type to a parameter that expects an object, or you are taking an object and converting it to a value type. However, boxing does not occur when you call a method on a value type. There is no conversion to an object, so if you need to assign an integer to a string using the ToString method, there is no boxing of the integer value as part of the creation of the string. Conversely, you are explicitly creating a new string object, so the cost is similar.

# GENERICS

Generics refer to the technology built into the .NET Framework (introduced originally with the .NET Framework version 2.0) that enables you to define a template and then declare variables using that template. The template defines the operations that the new type can perform; and when you declare a variable based on the template, you are creating a new type. The benefit of generics over untyped collections or arrays is that a generic template makes it easier for collection types to be strongly typed. The introduction of covariance in .NET Framework 4 makes it easier to reuse the template code in different scenarios.

The primary motivation for adding generics to .NET was to enable the creation of strongly typed collection types. Because generic collection types are strongly typed, they are significantly faster than the previous inheritance-based collection model. Anywhere you presently use collection classes in your code, you should consider revising that code to use generic collection types instead.

Visual Basic 2010 allows not only the use of preexisting generics, but also the creation of your own generic templates. Because the technology to support generics was created primarily to build collection classes, it