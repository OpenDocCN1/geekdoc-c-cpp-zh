
Inside Main - Before Callee: a = 20
Inside Callee a : 5
Inside Main - After Callee: a = 20
Inside Main - Before CalleeRef: a = 20
Inside CalleeRef a : 6
Inside Main - After CalleeRef: a = 6
Inside Main - Before CalleeOut: a = 6
Inside CalleeOut a : 7
Inside Main - After CalleeOut: a = 7

## Section 31.2: Changing values elsewhere

```
public static void Main(string[] args)
{
    var studentList = new List<Student>();
    studentList.Add(new Student("Scott", "Nuke"));
    studentList.Add(new Student("Vincent", "King"));
    studentList.Add(new Student("Craig", "Brett"));

    // make a separate list to print out later
    var printingList = studentList; // this is a new list object, but holding the same student objects inside it

    // oops, we've noticed typos in the names, so we fix those
    studentList[0].LastName = "Duke";
    studentList[1].LastName = "Kong";
    studentList[2].LastName = "Brett";

    // okay, we now print the list
    PrintPrintingList(printingList);
}
```

```
private static void PrintPrintingList(List<Student> students)
{
    foreach (Student student in students)
    {
        Console.WriteLine(string.Format("{0} {1}", student.FirstName, student.LastName));
    }
}
```

You'll notice that even though the printingList list was made before the corrections to student names after the typos, the PrintPrintingList method still prints out the corrected names:

Scott Duke
Vincent Kong
Craig Brett

This is because both lists hold a list of references to the same students. So changing the underlying student object propagates to usages by either list.

Here's what the student class would look like.

```
public class Student
{
    public string FirstName { get; set; }
    public string LastName { get; set; }

    public Student(string firstName, string lastName)
    {
        this.FirstName = firstName;
        this.LastName = lastName;
    }
}
```

## Section 31.3: ref vs out parameters

### Code

```
class Program
{
    static void Main(string[] args)
    {
        int a = 20;
        Console.WriteLine("Inside Main - Before Callee: a = {0}", a);
        Callee(a);
        Console.WriteLine("Inside Main - After Callee: a = {0}", a);
        Console.WriteLine();

        Console.WriteLine("Inside Main - Before CalleeRef: a = {0}", a);
        CalleeRef(ref a);
        Console.WriteLine("Inside Main - After CalleeRef: a = {0}", a);
        Console.WriteLine();

        Console.WriteLine("Inside Main - Before CalleeOut: a = {0}", a);
        CalleeOut(out a);
        Console.WriteLine("Inside Main - After CalleeOut: a = {0}", a);
        Console.ReadLine();
    }

    static void Callee(int a)
    {
        a += 5;
        Console.WriteLine("Inside Callee a : {0}", a);
    }

    static void CalleeRef(ref int a)
    {
        a += 10;
        Console.WriteLine("Inside CalleeRef a : {0}", a);
    }

    static void CalleeOut(out int a)
    {
        // can't use a+=15 since for this method 'a' is not initialized only declared in the method declaration
        a = 25; //has to be initialized
        Console.WriteLine("Inside CalleeOut a : {0}", a);
    }
}
```

### Output

```
Inside Main - Before Callee: a = 20
Inside Callee a : 25
Inside Main - After Callee: a = 20

Inside Main - Before CalleeRef: a = 20
Inside CalleeRef a : 30
Inside Main - After CalleeRef: a = 30
```

Inside Main - Before CalleeOut: a = 30
Inside CalleeOut a : 25
Inside Main - After CalleeOut: a = 25

## Section 31.4: Assignment

```
var a = new List<int>();
var b = a;
a.Add(5);
Console.WriteLine(a.Count); // prints 1
Console.WriteLine(b.Count); // prints 1 as well
```

Assigning to a variable of a List<int> does not create a copy of the List<int>. Instead, it copies the reference to the List<int>. We call types that behave this way reference types.

## Section 31.5: Difference with method parameters ref and out

There are two possible ways to pass a value type by reference: ref and out. The difference is that by passing it with ref the value must be initialized but not when passing it with out. Using out ensures that the variable has a value after the method call:

```
public void ByRef(ref int value)
{
    Console.WriteLine(nameof(ByRef) + value);
    value += 4;
    Console.WriteLine(nameof(ByRef) + value);
}
```

```
public void ByOut(out int value)
{
    value += 4; // CS0269: Use of unassigned out parameter `value'
    Console.WriteLine(nameof(ByOut) + value); // CS0269: Use of unassigned out parameter `value'

    value = 4;
    Console.WriteLine(nameof(ByOut) + value);
}
```

```
public void TestOut()
{
    int outValue1;
    ByOut(out outValue1); // prints 4

    int outValue2 = 10;  // does not make any sense for out
    ByOut(out outValue2); // prints 4
}
```

```
public void TestRef()
{
    int refValue1;
    ByRef(ref refValue1); // S0165  Use of unassigned local variable 'refValue'

    int refValue2 = 0;
    ByRef(ref refValue2); // prints 0 and 4

    int refValue3 = 10;
    ByRef(ref refValue3); // prints 10 and 14
}
```

The catch is that by using out the parameter must be initialized before leaving the method, therefore the following method is possible with ref but not with out:

```
```csharp
public void EmptyRef(bool condition, ref int value)
{
    if (condition)
    {
        value += 10;
    }
}

public void EmptyOut(bool condition, out int value)
{
    if (condition)
    {
        value = 10;
    }
} // CS0177: The out parameter 'value' must be assigned before control leaves the current method
```
```

This is because if condition does not hold, value goes unassigned.

## Section 31.6: Passing by reference

If you want the Value Types vs Reference Types in methods example to work properly, use the ref keyword in your method signature for the parameter you want to pass by reference, as well as when you call the method.

```
```csharp
public static void Main(string[] args)
{
    ...
    DoubleNumber(ref number); // calling code
    Console.WriteLine(number); // outputs 8
    ...
}
```
```

```
```csharp
public void DoubleNumber(ref int number)
{
    number += number;
}
```
```

Making these changes would make the number update as expected, meaning the console output for number would be 8.

## Chapter 32: Built-in Types

### Section 32.1: Conversion of boxed value types

Boxed value types can only be unboxed into their original Type, even if a conversion of the two Types is valid, e.g.:

```
object boxedInt = (int)1; // int boxed in an object
long unboxedInt1 = (long)boxedInt; // invalid cast
```

This can be avoided by first unboxing into the original Type, e.g.:

```
long unboxedInt2 = (long)(int)boxedInt; // valid
```

### Section 32.2: Comparisons with boxed value types

If value types are assigned to variables of type object they are boxed - the value is stored in an instance of a System.Object. This can lead to unintended consequences when comparing values with ==, e.g.:

```
object left = (int)1; // int in an object box
object right = (int)1; // int in an object box
var comparison1 = left == right; // false
```

This can be avoided by using the overloaded Equals method, which will give the expected result.

```
var comparison2 = left.Equals(right); // true
```

Alternatively, the same could be done by unboxing the left and right variables so that the int values are compared:

```
var comparison3 = (int)left == (int)right; // true
```

### Section 32.3: Immutable reference type - string

```
// assign string from a string literal
string s = "hello";

// assign string from an array of characters
char[] chars = new char[] { 'h', 'e', 'l', 'l', 'o' };
string s = new string(chars, 0, chars.Length);

// assign string from a char pointer, derived from a string
string s;
unsafe
{
    fixed (char* charPointer = "hello")
    {
        s = new string(charPointer);
    }
}
```

### Section 32.4: Value type - char

```
// single character s
char c = 's';

// character s: casted from integer value
char c = (char)115;

// unicode character: single character s
char c = '\u0073';

// unicode character: smiley face
char c = '\u263a';
```

### Section 32.5: Value type - short, int, long (signed 16 bit, 32 bit, 64 bit integers)

```
// assigning a signed short to its minimum value
short s = -32768;

// assigning a signed short to its maximum value
short s = 32767;

// assigning a signed int to its minimum value
int i = -2147483648;

// assigning a signed int to its maximum value
int i = 2147483647;

// assigning a signed long to its minimum value (note the long postfix)
long l = -9223372036854775808L;

// assigning a signed long to its maximum value (note the long postfix)
long l = 9223372036854775807L;
```

It is also possible to make these types nullable, meaning that additionally to the usual values, null can be assigned, too. If a variable of a nullable type is not initialized, it will be null instead of 0. Nullable types are marked by adding a question mark (?) after the type.

```
int a; //This is now 0.
int? b; //This is now null.
```

### Section 32.6: Value type - ushort, uint, ulong (unsigned 16 bit, 32 bit, 64 bit integers)

```
// assigning an unsigned short to its minimum value
ushort s = 0;

// assigning an unsigned short to its maximum value
ushort s = 65535;

// assigning an unsigned int to its minimum value
uint i = 0;

// assigning an unsigned int to its maximum value
uint i = 4294967295;
```
