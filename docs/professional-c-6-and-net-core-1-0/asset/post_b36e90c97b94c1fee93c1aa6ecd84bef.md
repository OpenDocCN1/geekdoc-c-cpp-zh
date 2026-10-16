
You can overload generic methods to define specializations for specific types. This is true for methods with generic parameters as well. The Foo method is defined in four versions. The first accepts a generic parameter; the second one is a specialized version for the int parameter. The third Foo method accepts two generic parameters, and the fourth one is a specialized version of the third one with the first parameter of type int. During compile time, the best match is taken. If an int is passed, then the method with the int parameter is selected. With any other parameter type, the compiler chooses the generic version of the method (code file Specialization/Program.cs):

```
public class MethodOverloads
{
    public void Foo<T>(T obj)
    {
        WriteLine($"Foo<T>(T obj), obj type: {obj.GetType().Name}");
    }

    public void Foo(int x)
    {
        WriteLine("Foo(int x)");
    }

    public void Foo<T1, T2>(T1 obj1, T2 obj2)
    {
        WriteLine($"Foo<T1, T2>(T1 obj1, T2 obj2); {obj1.GetType().Name}" +
            $"{obj2.GetType().Name}");
    }

    public void Foo<T>(int obj1, T obj2)
    {
        WriteLine($"Foo<T>(int obj1, T obj2); {obj2.GetType().Name}");
    }

    public void Bar<T>(T obj)
    {
        Foo(obj);
    }
}
```

The Foo method can now be invoked with any parameter type. The sample code passes int and string values to invoke all four Foo methods:

```
static void Main()
{
    var test = new MethodOverloads();
    test.Foo(33);
    test.Foo("abc");
    test.Foo("abc", 42);
    test.Foo(33,"abc");
}
```

Running the program, you can see by the output that the method with the best match is taken:

```
Foo(int x)
Foo<T>(T obj), obj type: String
```

## 7 Arrays and Tuples

### What’s In This Chapter?

- Simple arrays
- Multidimensional arrays
- Jagged arrays
- The `Array` class
- Arrays as parameters
- Enumerations
- Tuples
- Structural comparison

### Wrox.com Code Downloads for This Chapter

The wrox.com code downloads for this chapter are found at [www.wrox.com/go/professionalcsharp6](www.wrox.com/go/professionalcsharp6) on the Download Code tab. The code for this chapter is divided into the following major examples:

- SimpleArrays
- SortingSample
- ArraySegment
- YieldsSample
- TuplesSample
- StructuralComparison

### Multiple Objects of the Same and Different Types

If you need to work with multiple objects of the same type, you can use collections (see Chapter 11, “Collections”) and arrays. C# has a special notation to declare, initialize, and use arrays. Behind the scenes, the `Array` class comes into play, which offers several methods to sort and filter the elements inside the array. Using an enumerator, you can iterate through all the elements of the array.

To use multiple objects of different types, the type `Tuple` can be used. See the “Tuples” section later in this chapter for details about this type.

### Simple Arrays

If you need to use multiple objects of the same type, you can use an array. An array is a data structure that contains a number of elements of the same type.

### Array Declaration

An array is declared by defining the type of elements inside the array, followed by empty brackets and a variable name. For example, an array containing integer elements is declared like this:

```
int[] myArray;
```

### Array Initialization

After declaring an array, memory must be allocated to hold all the elements of the array. An array is a reference type, so memory on the heap must be allocated. You do this by initializing the variable of the array using the new operator, with the type and the number of elements inside the array. Here, you specify the size of the array:

```
myArray = new int[4];
```

> NOTE Value types and reference types are covered in Chapter 3, “Objects and Types.”

With this declaration and initialization, the variable myArray references four integer values that are allocated on the managed heap (see Figure 7.1).

![](img/3d365b72b289213a91ade7eb366b8f35_271_0.png)

> NOTE An array cannot be resized after its size is specified without copying all the elements. If you don’t know how many elements should be in the array in advance, you can use a collection (see Chapter 11).

Instead of using a separate line to declare and initialize an array, you can use a single line:

```
int[] myArray = new int[4];
```

You can also assign values to every array element using an array initializer. You can use array initializers only while declaring an array variable, not after the array is declared:

```
int[] myArray = new int[4] {4, 7, 11, 2};
```

If you initialize the array using curly brackets, you can also omit the size of the array because the compiler can count the number of elements:

```
int[] myArray = new int[] {4, 7, 11, 2};
```

There’s even a shorter form using the C# compiler. Using curly brackets you can write the array declaration and initialization. The code generated from the compiler is the same as the previous result:

```
int[] myArray = {4, 7, 11, 2};
```

### Accessing Array Elements

After an array is declared and initialized, you can access the array elements using an indexer. Arrays support only indexers that have integer parameters.

With the indexer, you pass the element number to access the array. The indexer always starts with a value of 0 for the first element. Therefore, the highest number you can pass to the indexer is the number of elements minus one, because the index starts at zero. In the following example, the array myArray is declared and initialized with four integer values. The elements can be accessed with indexer values 0, 1, 2, and 3.

```
int[] myArray = new int[] {4, 7, 11, 2};
int v1 = myArray[0];    // read first element
int v2 = myArray[1];    // read second element
myArray[3] = 44;        // change fourth element
```

> NOTE If you use a wrong indexer value that is bigger than the length of the array, an exception of type IndexOutOfRangeException is thrown.

If you don’t know the number of elements in the array, you can use the Length property, as shown in this for statement:

```
for (int i = 0; i < myArray.Length; i++)
{
    WriteLine(myArray[i]);
}
```

Instead of using a for statement to iterate through all the elements of the array, you can also use the foreach statement:

```
foreach (var val in myArray)
{
    WriteLine(val);
}
```

> NOTE The foreach statement makes use of the IEnumerable and IEnumerator interfaces and traverses through the array from the first index to the last. This is discussed in detail later in this chapter.

### Using Reference Types

In addition to being able to declare arrays of predefined types, you can also declare arrays of custom types. Let’s start with the following Person class, the properties FirstName and LastName using auto-implemented properties, and an override of the ToString method from the Object class (code file SimpleArrays/Person.cs):

```csharp
public class Person
{
    public string FirstName { get; set; }
    public string LastName { get; set; }

    public override string ToString() => $"{FirstName} {LastName}";
}
```

Declaring an array of two Person elements is similar to declaring an array of int:

```csharp
Person[] myPersons = new Person[2];
```

However, be aware that if the elements in the array are reference types, memory must be allocated for every array element. If you use an item in the array for which no memory was allocated, a NullReferenceException is thrown.

> NOTE For information about errors and exceptions, see Chapter 14, “Errors and Exceptions.”

You can allocate every element of the array by using an indexer starting from 0:

```csharp
myPersons[0] = new Person { FirstName="Ayrton", LastName="Senna" };
myPersons[1] = new Person { FirstName="Michael", LastName="Schumacher" };
```

Figure 7.2 shows the objects in the managed heap with the Person array. myPersons is a variable that is stored on the stack. This variable references an array of Person elements that is stored on the managed heap. This array has enough space for two references. Every item in the array references a Person object that is also stored in the managed heap.
