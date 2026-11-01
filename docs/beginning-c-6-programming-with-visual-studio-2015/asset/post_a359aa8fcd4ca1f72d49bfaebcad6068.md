
> > **NOTE** Interestingly, multiplying two short values together doesn’t return a short value. Because the result of this operation is quite likely to exceed 32767 (the maximum value a short can hold), it actually returns an int.
> >
> > The conversion process can seem complex at first glance, but as long as you break expressions down into parts by taking the operator precedence order into account, you should be able to work things out.

## COMPLEX VARIABLE TYPES

In addition to all the simple variable types, C# also offers three slightly more complex (but very useful) sorts of variables: enumerations (often referred to as enums), structs (occasionally referred to as structures), and arrays.

### Enumerations

Each of the types you’ve seen so far (with the exception of `string`) has a clearly defined set of allowed values. Admittedly, this set is so large in types such as double that it can practically be considered a continuum, but it is a fixed set nevertheless. The simplest example of this is the bool type, which can take only one of two values: `true` or `false`.

There are many other circumstances in which you might want to have a variable that can take one of a fixed set of results. For example, you might want to have an orientation type that can store one of the values north, south, east, or west.

In situations like this, *enumerations* can be very useful. Enumerations do exactly what you want in this orientation type: They allow the definition of a type that can take one of a finite set of values that you supply. What you need to do, then, is create your own enumeration type called orientation that can take one of the four possible values.

Note that there is an additional step involved here — you don’t just declare a variable of a given type; you declare and detail a user-defined type and then declare a variable of this new type.

### Defining Enumerations

You can use the enum keyword to define enumerations as follows:

```
enum <typeName>
{
    <value1>,
    <value2>,
    <value3>,
    ...
    <valueN>
}
```

Note that this can cause problems, with values specified after a definition such as <value2> = <value1> being identical to other values. For example, in the following code <value4> will have the same value as <value2>:

```
enum <typeName> : <underlyingType>
{
    <value1> = <actualVal1>,
    <value2>,
    <value3> = <value1>,
    <value4>,
    ...
    <valueN> = <actualValN>
}
```

Of course, if this is the behavior you want, then this code is fine. Note also that assigning values in a circular fashion will cause an error:

```
enum <typeName> : <underlyingType>
{
    <value1> = <value2>,
    <value2> = <value1>
}
```

The following Try It Out shows an example of all of this. The code defines and then uses an enumeration called orientation.

### TRY IT OUT Using an Enumeration: Ch05Ex02\Program.cs

- 1. Create a new console application called Ch05Ex02 and save it in the directory C:\BegVCSharp\Chapter05.
- 2. Add the following code to Program.cs:

```
namespace Ch05Ex02
{
    enum orientation : byte
    {
        north = 1,
        south = 2,
        east = 3,
        west = 4
    }
    class Program
    {
        static void Main(string[] args)
        {
            orientation myDirection = orientation.north;
            WriteLine($"myDirection = {myDirection}");
            ReadKey();
        }
    }
}
```

### Defining Structs

Structs are defined using the struct keyword as follows:

```
struct <typeName>
{
    <memberDeclarations>
}
```

The <memberDeclarations> section contains declarations of variables (called the data members of the struct) in almost the same format as usual. Each member declaration takes the following form:

```
<accessibility> <type> <name>;
```

To allow the code that calls the struct to access the struct's data members, you use the keyword public for <accessibility>. For example:

```
struct route
{
    public orientation direction;
    public double      distance;
}
```

Once you have a struct type defined, you use it by defining variables of the new type:

```
route myRoute;
```

In addition, you have access to the data members of this composite variable via the period character:

```
myRoute.direction = orientation.north;
myRoute.distance  = 2.5;
```

This is demonstrated in the following Try It Out, where the orientation enumeration from the last Try It Out is used with the route struct shown earlier. This struct is then manipulated in code to give you a feel for how structs work.

### TRY IT OUT Using a Struct: Ch05Ex03\Program.cs

- 1. Create a new console application called Ch05Ex03 and save it in the directory C:\BegVCSharp\Chapter05.
- 2. Add the following code to Program.cs:

```
namespace Ch05Ex03
{
    enum orientation: byte
    {
        north = 1,
        south = 2,
        east = 3,
        west = 4
    }
    struct route
    {
        public orientation direction;
        public double distance;
    }
    class Program
    {
        static void Main(string[] args)
        {
            route myRoute;
            int myDirection = -1;
            double myDistance;
            WriteLine("1) North\n2) South\n3) East\n4) West");
            do
            {
                WriteLine("Select a direction:");
                myDirection = ToInt32(ReadLine());
            }
            while ((myDirection < 1) || (myDirection > 4));
            WriteLine("Input a distance:");
            myDistance = ToDouble(ReadLine());
            myRoute.direction = (orientation)myDirection;
            myRoute.distance = myDistance;
            WriteLine($"myRoute specifies a direction of {myRoute.direction} " +
            $"and a distance of {myRoute.distance}");
            ReadKey();
        }
    }
}
```

- 3. Execute the code, select a direction by entering a number between 1 and 4, and then enter a distance. The result is shown in Figure 5-7.

![](img/cf72ea860016d2d680fc085fc06f265a_118_0.png)

FIGURE 5-7

### How It Works

Structs, like enumerations, are declared outside of the main body of the code. You declare your route struct just inside the namespace declaration, along with the orientation enumeration that it uses:

```
enum orientation: byte
{
    north = 1,
    south = 2,
    east = 3,
    west = 4
}
```

In addition, you can combine these two methods of initialization if you want:

```csharp
int[] myIntArray = new int[5] { 5, 9, 10, 2, 99 };
```

With this method the sizes must match. You can't, for example, write the following:

```csharp
int[] myIntArray = new int[10] { 5, 9, 10, 2, 99 };
```

Here, the array is defined as having 10 members, but only five are defined, so compilation will fail. A side effect of this is that if you define the size using a variable, then that variable must be a constant:

```csharp
const int arraySize = 5;
int[] myIntArray = new int[arraySize] { 5, 9, 10, 2, 99 };
```

If you omit the const keyword, this code will fail.

As with other variable types, there is no need to initialize an array on the same line that you declare it. The following is perfectly legal:

```csharp
int[] myIntArray;
myIntArray = new int[5];
```

In the following Try It Out you create and use an array of strings, using the example from the introduction to this section.

### TRY IT OUT Using an Array: Ch05Ex04\Program.cs

- 1. Create a new console application called Ch05Ex04 and save it in the directory C:\BegVCSharp\Chapter05.
- 2. Add the following code to Program.cs:
- 3. Execute the code. The result is shown in Figure 5-8.

```csharp
static void Main(string[] args)
{
    string[] friendNames = { "Todd Anthony", "Kevin Holton",
        "Shane Laigle" };
    int i;
    WriteLine($"Here are {friendNames.Length} of my friends:");
    for (i = 0; i < friendNames.Length; i++)
    {
        WriteLine(friendNames[i]);
    }
    ReadKey();
}
```

![](img/cf72ea860016d2d680fc085fc06f265a_121_0.png)
