
## Getting hexed

Like binary numbers (0 and 1), hexadecimal, or "hex," numbers are fundamental to computer programming. In base 16, the digits are 0 through 9 and then A, B, C, D, E, F — where A=10, B=11 ... F=15. To illustrate (using the zero-x prefix to indicate hex):

```
0x2A = 42 decimal: 2*16 + A*1 (where A*1 = 10*1)
```

The alphabetic digits can be uppercase or lowercase: C is the same as c. It's weird, but quite useful, especially when you're debugging or working close to the metal with memory contents.

```
0xD = 13 decimal
0x10 = 16 decimal: 1*16 + 0*1
```

At the end of the loop, it pauses to allow the programmer a chance to gaze on the output from DumpHex().

The GetFileList() method begins by creating an empty FileInfo list. This list is the one it returns in the event of an error.

Here's a neat trick to remember when coding any Get...List() method: If an error occurs, display an error message and return a zero-length list.

![](img/80ff26f06fc9ab951e1cd4257b867366_162_0.png)

![](img/80ff26f06fc9ab951e1cd4257b867366_162_1.png)

Be careful about returning a reference to an object. For instance, don't return a reference to one of the underlying queues wrapped up in the PriorityQueue class, described in Chapter 8 of this minibook — unless you want to invite folks to mess with those queues through the reference instead of through your class methods, that is. That's a sure ticket to a corrupt, unpredictable queue. But GetFileList() doesn't expose the innards of one of your classes here, so it's okay.

GetFileList() then creates a DirectoryInfo object. Just as its name implies, a DirectoryInfo object contains the same type of information about a directory that a FileInfo object does about a file: name, rank, and serial-number-type stuff. However, the DirectoryInfo object has access to one thing that a FileInfo doesn't: a list of the files in the directory, in the form of a FileInfo array.

As usual, GetFileList() wraps the directory- and file-related code in a big try block. (For an explanation of try and catch, see Chapter 9 in this minibook.) The catch at the end traps any errors that are generated. Just to embarrass you further, the catch block flaunts the name of the directory (which probably doesn't exist, because you entered it incorrectly).

The DumpHex() method is a little tricky only because of the difficulties in formatting the output just right.

DumpHex() starts out by opening the file. A FileInfo object contains information about the file — it doesn't open the file. DumpHex() gets the full name of the file, including the path, and then opens a FileStream in read-only mode using that name. The catch block throws an exception if FileStream can't read the file for some reason.

DumpHex() then reads through the file, 10 bytes at a time. It displays every 10 bytes in hexadecimal format as a single line. Every 20 lines, it pauses until the user presses Enter. I use the modulo operator, %, to accomplish that task.

![](img/80ff26f06fc9ab951e1cd4257b867366_163_0.png)

Vertically, a console window has room for 25 lines by default. (The user can change the window's size, of course, allowing more or fewer lines.) That means you have to pause every 20 lines or so. Otherwise, the data just streams off the top of the screen before the user can read it.

The modulo operator (%) returns the remainder after division. Thus (line % 20) == 0 is true when line equals 20, 40, 60, 80 — you get the idea. This trick is valuable, useful in all sorts of looping situations where you want to perform an operation only so often.

DumpBuffer() writes out each member of a byte array using the X2 format control. Although X2 sounds like the name of a secret military experiment, it simply means "display a number as two hexadecimal digits."

The range of a byte is 0 to 255, or 0xFF — two hex digits per byte.

Here are the first 20 lines of the output.txt file (even its own mother wouldn't recognize this picture):

```
Hex dump of file C:\C#Programs\Vi\holdtank\Test2\bin\output.txt:
001 - 53, 74, 65, 63, 6D, 20, 28, 70, 72,
002 - 6F, 74, 65, 63, 74, 65, 64, 20, 29, 0D, 0A,
003 - 20, 20, 26, 69, 6C, 65, 53, 72, 74, 72, 65,
004 - 61, 6D, 28, 73, 74, 72, 69, 6E, 67, 2C,
005 - 20, 46, 69, 6C, 65, 4D, 61, 41, 63, 63, 65, 73, 73,
006 - 20, 20, 46, 69, 6C, 65, 4D, 61, 41, 63, 63, 65, 73, 73,
007 - 73, 29, 0D, 0A, 20, 20, 20, 20, 40, 6D, 6F,
008 - 72, 79, 73, 74, 72, 65, 61, 6C, 20, 29, 0D, 0A,
009 - 3B, 0D, 0A, 20, 20, 20, 20, 48, 77, 74, 74, 67,
010 - 72, 6B, 53, 74, 74, 72, 65, 65, 61, 6D, 0D, 0A,
011 - 20, 20, 20, 42, 75, 66, 66, 65, 72, 72, 73, 72, 74,
012 - 72, 65, 65, 61, 6D, 20, 20, 2D, 62, 75, 65, 66,
013 - 66, 65, 75, 72, 73, 20, 61, 61, 66, 20, 65, 78, 78,
014 - 69, 73, 74, 74, 74, 6E, 67, 20, 20, 73, 74, 74, 72,
015 - 65, 65, 61, 6D, 20, 20, 69, 62, 62, 62, 66, 65, 74, 74,
016 - 0D, 0A, 0D, 0A, 42, 69, 6E, 6D, 61, 72, 72, 79,
017 - 52, 65, 65, 51, 64, 65, 65, 20, 20, 2D, 20, 72,
018 - 65, 65, 51, 64, 20, 69, 69, 69, 6E, 20, 20, 76, 61, 72,
019 - 69, 69, 66, 65, 73, 73, 20, 74, 79, 79, 70, 65, 73, 73,
020 - 20, 20, 28, 28, 68, 61, 61, 72, 2C, 20, 20, 49, 6E,
Enter return to continue another 20 lines
```

![](img/80ff26f06fc9ab951e1cd4257b867366_164_0.png)

You could reconstruct the file as a string from the hex display. The 0x61 value is the numeric equivalent of the character a. The letters of the alphabet are arranged in order, so 0x65 should be the character e; 0x20 is a space. The first line in this example (after the line number) is `s} \n\r Nemo`, where \n is a new line and \r is a carriage return. Intriguing, eh? That's about as far as I want to go. You can search Google or another search engine for an ASCII table.

Those codes are also valid for the lower part of the much vaster Unicode character set, which C# uses by default. (You can look on a search engine on the web for the term Unicode characters, and I explain the basics in the article “Converting Between Byte and Char Arrays” on the http://csharp102.info website.)

The following example shows what happens when the user specifies the invalid directory x:

```
Directory "x" invalid
Could not find a part of the path "C:\C#Programs\LoopThroughFiles\bin\Debug\x".

No files left
Press Enter to terminate...
```

Impressive, no?

## Iterating foreach Collections: Iterators

In the rest of this chapter, you see three different approaches to the general problem of iterating a collection. In this section, I continue discussing the most traditional approach (at least for C# programmers), the iterator class, or enumerator, which implements the IEnumerator interface.

![](img/80ff26f06fc9ab951e1cd4257b867366_164_1.png)

The terms iterator and enumerator are synonymous. The term iterator is more common despite the name of the interface, but enumerator has been popular at Microsoft. Verb forms of these two nouns are also available: You iterate or enumerate through a container or collection. Note that the indexers and the new iterator blocks discussed later in this chapter are other approaches to the same problem.

### Accessing a collection: The general problem

Different collection types may have different accessing schemes. Not all types of collections can be accessed efficiently with an index like an array’s — the linked list, for example. A linked list just contains a reference to the next item in the list and is made to be consecutively — not randomly — accessed. Differences between collection types make it impossible to write a method such as the following without special provisions:

```csharp
// Pass in any kind of collection:
void MyClearMethod(Collection aColl, int index)
{
    aColl[index] = 0; // Indexing doesn't work for all types of collections.
    // ... continues ...
}
```

Each collection type can (and does) define its own access methods. For example, a linked list may offer a `GetNext()` method to fetch the next element in the chain of objects or a stack notation may offer a `Push()` and `Pop()` to add and remove objects.

A more general approach is to provide for each collection class a separate *iterator* class, which is wise in the ways of navigating that particular collection. Each collection X defines its own class `IteratorX`. Unlike X, `IteratorX` offers a common `IEnumerator` interface, the gold standard of iterating. This technique uses a second object, the *iterator*, as a kind of pointer, or cursor, into the collection.

The iterator (enumerator) approach offers these advantages:

- Each collection class can define its own iteration class. Because the iteration class implements the standard `IEnumerator` interface, it’s usually straightforward to code.
- The application code doesn’t need to know how the collection code works. As long as the programmer understands how to use the iterator, the iteration class can handle the details. That’s good encapsulation.
- The application code can create multiple independent iterator objects for the same collection. Because the iterator contains its own state information (“knows where it is,” in the iteration), each iterator can navigate through the collection independently. You can have several iterations going at one time, each one at a different location in the collection.

To make the `foreach` loop possible, the `IEnumerator` interface must support all different types of collections, from arrays to linked lists. Consequently, its methods must be as general as possible. For example, you can’t use the iterator to access locations within the collection class randomly because most collections don’t provide random access. (You’d need to invent a different enumeration interface with that ability, but it wouldn’t work with `foreach`.)

`IEnumerator` provides these three methods:

- `Reset()`: Sets the enumerator to point to the beginning of the collection. **Note:** The generic version of `IEnumerator`, `IEnumerator<T>`, doesn’t provide a `Reset()` method. With .NET’s generic `LinkedList`, for example, just begin with a call to `MoveNext()`. That generic `LinkedList` is found in `System.Collections.Generic`.
