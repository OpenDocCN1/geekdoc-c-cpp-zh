148 Input and Output

# 25.2 Overview of Input and Output Methods

The following table summarizes the naming conventions for methods of the input and output classes as well as their main characteristics, such as their end-of-stream behavior.

| Method Name | Effect |
| --- | --- |
| Read | Inputs characters from a TextReader (section 25.4) or inputs bytes from a Stream (section 25.7) or one character from a BinaryReader (section 25.6). It blocks, that is, does not return, until some input is available; Returns – 1 on end-of-stream, except for the Read(byte[], ...) overloads, which return 0. |
| Readt | Inputs a value of type i from a BinaryReader (section 25.6). Blocks until some input is available; throws EndStream on end-of-stream. |
| Peek | Returns the next character from a TextReader (section 25.4) without advancing the stream. Blocks until some input is available; returns –1 on end-of-stream. |
| PeekChar | Returns the next character from a BinaryReader (section 25.6) without advancing the stream. Blocks until some input is available; returns –1 on end-of-stream. |
| Write | Outputs the text representation of a value (of type int, double, ..., String Object) to a TextWriter which outputs bytes to a Stream (section 25.7) or outputs the representation of a value to a BinaryReader (section 25.6). |
| WriteLine | Same as Write but outputs a newline after each call. |
| Flush | Writes buffered data that has been written to the file system or network. |
| Close | Flushes the stream and releases resources held by the stream. Further operations on the stream, except Close, may throw an ObjectDisException. Writers and output streams should be explicitly closed to make sure that all data have been written to disk or network; otherwise output may be lost. |
| Deserialize | Deserializes objects from a Stream (examples 184 and 254). Defined in System.Runtime.Serialization.Formatters.Binary.BinaryFormatter and System.Runtime.Serialization.Formatters.SoapFormatter. |
| Serialize | Serializes objects to a Stream (examples 184 and 254). Defined in System.Runtime.Serialization.Formatters.BinaryFormatter and System.Runtime.Serialization.Formatters.SoapFormatter. |

# 25.3 Using Declarations, Exceptions, Thread Safety

A program using the input and output classes must contain the declaration
using System.IO;

Most input and output operations can throw an exception of IOException or one of its subclasses (section 20). Hence a method doing input or output should be in a try-catch block (section 13.8.2).
The standard implementation of input-output is not thread-safe; multiple concurrent threads (section 21) cannot read from or write to the stream without corrupting it; so one should not use the same stream from multiple threads. Classes TextReader and TextWriter have a static method Synchronized for creating thread-safe readers and writers.