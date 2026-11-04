
|  |  |  |
|---|---|---|
| Extra = "This is good bye";<br>if(Extra.Substring(0,<br>4).CompareTo(S.Substring(0, 4)) ==<br>0)<br>Console.WriteLine("They match!");<br>else<br>Console.WriteLine<br>("They don't match!"); } } | string S("This is a<br>string\n"),<br>S1("This is a string\n"),<br>S2("Is this string larger?<br>\n");<br>T = S1.compare(0,<br>S1.size(), S2, 0,<br>S2.size());<br>if(T &gt; 0)<br>cout &lt;&lt; "S2 is greater"<br>&lt;&lt; endl; }<br>Where 0 to S1.size()<br>equals the length of S1,<br>and 0 to S2 equals the<br>length of the<br>comparison. | S1[ ] = "This is a string\n";<br>S2[ ] = "This is a string of<br>data\n";<br>if(strcmp(S1, S2) &lt; 0)<br>std::cout &lt;&lt; "Super array is<br>better \n";<br>if(strcmp(S1, SuperArray, 4)<br>== 0)<br>std::cout &lt;&lt; "Are first 4 letter<br>are equal \n"; } |
| Determines the length of a string<br>using System;<br>namespace Chapter4<br>{ class Class1<br>{ static void Main()<br>{ string S = "This is a string\n";<br>int ArrayLength = S.Length;<br>Console.WriteLine(S.Length);<br>} } } | #include &lt;iostream&gt;<br>#include &lt;string&gt;<br>using namespace std;<br>void main(void)<br>{ string String1;<br>std::cout &lt;&lt; "Enter a<br>string: \n";<br>std::getline(cin,<br>String1);<br>int Length = | #include &lt;iostream&gt;<br>#include &lt;cstring&gt;<br>using namespace std;<br>void main(void)<br>{ const int array_size = 100;<br>int length;<br>char Array[array_size];<br>std::cout &lt;&lt;<br>"Enter a test sentence. \n";<br>std::cin.getline(Array, |

> There are dozens more, all quickly accessible from the visual compiler's pop-up menu.

### Converting and Safeguarding Data

In addition to inputting and manipulating data, we can also convert and safeguard against data input errors. For example, when our users need to input numeric data, we can use the broader string data type and then test and convert that data as necessary. The data comparison functions are quite numerous, as shown in Table 4.2.

| Commands/Examples | Description |
|---|---|
| `char.IsLetterOrDigit` | Returns true when an alphanumeric character (A-Z, a-z, 0-9) is found. |
| `char.IsLetter` | Returns true when an alphabetic character (A-Z or a-z) is found. |
| `char.IsSymbol` | Returns true when a character is found to be a symbol. |
| `char.IsControl` | Returns true when a control character (0x00-0x1F or 0x7F) is found. |
| `char.IsSeparator` | Returns true when a separator character is found. |
| `char.IsSurrogate` | Returns true when a surrogate character is found. |
| `char.IsDigit, char.IsNumber` | Returns a nonzero value when a decimal (0-9) is found. |
| `char.IsLower` | Returns true when a lowercase alphabetical character is found. |
| `char.IsPunctuation` | Returns true when a punctuation mark is found. |
| `char.IsWhiteSpace` | Returns true when a whitespace character is found. |
| `char.IsUpper` | Returns true when an uppercase alphabetical character is found. |

Table 4.2. Data comparison functions.

![](img/bdd7d3d10cc8dfc1d71aaaf7003fc32b_289_0.png)

In the ancient times, many of the primitive C programmers fell victim to an unspeakable evil known as the Malloc.

## From Strings to Streams: System.IO

In addition to storing and retrieving simple character strings, we can also widen our perspective by beginning to access and write to files via our floppy and hard drives. The use of file manipulations also includes the addition of a second reference, System.IO, which enables the use of two key file-related methods: StreamReader and StreamWriter. These methods, as their names imply, allow us to read and write to those files. The files in question need to be opened and closed separately, that is, one reference is used to identify the file as a storage device and one to retrieve that data. As with many of the object-based functions, our data streams also offer a host of member accessible functions that will be explored as we uncover the Base Class Library. The correct procedure for accessing these methods always includes an opening statement, a reading or writing to statement, and the closing method (see Table 4.3). Note that forgetting to close these files will produce a runtime error.

| C# | C++ |
|---|---|
| using System;<br>using System.IO;<br><br>namespace Chapter4<br>{ class Class1<br>{ static void Main ()<br>{ StreamWriter SaveFile = new<br>StreamWriter(@"C:\MyFile.txt");<br>SaveFile.WriteLine("This is a test");<br>SaveFile.Close();<br><br>StreamReader ReadFile = new<br>StreamReader(@"C:\MyFile.txt");<br>string MyFile = ReadFile.ReadLine();<br>Console.WriteLine(MyFile);<br>ReadFile.Close(); } } | #include &lt;fstream.h&gt;<br>void main(void)<br>{ char output[80];<br>ofstream save;<br>save.open("File.dat");<br>save &lt;&lt; "This is a test";<br>save.close();<br>ifstream read;<br>read.open("File.dat");<br>if(read.fail())<br>{ cout &lt;&lt; "File not found!"<br>&lt;&lt; endl;<br>return; }<br>while(read.eof())<br>{ read &gt;&gt; output;<br>cout &lt;&lt; output &lt;&lt; " ";<br>cout &lt;&lt; endl;<br>read.close(); } |

**Table 4.3. StreamReader and StreamWriter.**

### Examining Object Types

Another important point when working with object types involves the use of extensions, which are methods that allow us to manipulate objects, including Equals ( ), GetHashCode ( ), GetType ( ), and ToString ( ). The use of extensions can determine a host of information and thus simplify our tasks (see Table 4.4).

| C# Type | Description |
|---|---|
| Boolean bool<br>Object.Equals(object obj) | Determines whether the specified Object is equal to the current Object. |
| Boolean bool<br>Object.GetHashCode(object obj) | Serves as a hash function for a particular type, suitable for use in hashing algorithms and data structures like a hash table |
| Boolean bool<br>Object.GetType(object obj) | Gets the type of the current instance |
| Boolean bool<br>Object.ToString(object obj) | Returns a string that represents the current object |

**Table 4.4. Extensions.**

### The Keywords checked and unchecked

Another weakness when programming in other computer languages is their inability to protect against arithmetic overflow. An arithmetic overflow occurs when a variable of a numeric data type exceeds its preset range. Once a value exceeds that range, its variable reference no longer produces the implied response, thus that program is considered corrupt and all its data considered invalid. To protect against such errors, the designers of C# implemented two options: first, we can include coding references such as the keywords checked and unchecked; second, we can include a generalized compiler reference that tests our code for us. To implement these references see Examples 4.38–4.40 and Screen Shot 4.5.

**Example 4.38. The keyword checked.**

```csharp
using System;

namespace Chapter4 {
    class Class1 {
        static void Main() {
            byte Max255 = 255;

            Max255++; // this error will go undetected

            checked { // this error will call an exception at run-time
                Max255++;
            }
        }
    }
}
```

![](img/bdd7d3d10cc8dfc1d71aaaf7003fc32b_291_0.png)

From the “Solution Explorer,” modify the program’s “Build” properties to include automatic checking and then execute this coding.

**Example 4.39. A checked compiler.**

```csharp
using System;

namespace Chapter4 {
    class Class1 {
        static void Main() {
            byte Max255 = 255;
            Max255 += 1; // this error will call an exception at run time
        }
    }
}
```

Continuing from the last program, override the system’s automatic checking with the keyword *unchecked* encasing the last block (see Example 4.40).

**Example 4.40. An unchecked compiler.**

```csharp
using System;

namespace Chapter4 {
    class Class1 {
        static void Main() {
            byte Max255 = 255;
            unchecked {
                Max255 += 1; // this error will go undetected
            }
        }
    }
}
```

### The goto Statement

The goto statement is probably the most picked-on of all the keywords. Its use is considered a poor programming habit, yet somehow it manages to endure. Its fault lies in its ability to transgress order—the C# help files even mark it as a useful way of getting out of nested statements, but, of course, that would be breaking the rules. Still, there is at least
