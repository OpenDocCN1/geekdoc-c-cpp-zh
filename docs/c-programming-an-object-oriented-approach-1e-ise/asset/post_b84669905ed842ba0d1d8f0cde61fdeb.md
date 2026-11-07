
![](img/d68f6199646ca63591a6d8419e0ed4ba_736_0.png)

## Role of Streams

One of the reasons that the C++ standard created input/output streams is to change bytes of data that are received from a source to the data type the program needs and to change the data types that the program sends to a sink into bytes that the sink can store. In other words, the main job of streams can be thought of as converting bytes to data types and data types to bytes. Of course streams have other jobs, such as controlling the flow of bytes in and out of the computer, as we will see gradually in this chapter. Figure 16.3 shows this idea.

## Text versus Binary Input/Output

When we input or output data, we must understand that three locations are involved: memory, a stream, and a source/sink. We now examine how data are stored in these three locations.

**Storage of Data in Memory** The memory of a computer is a collection of bytes (8-bit) chunks, but we do not store data as individual bytes; we store data as a set of contiguous bytes. For example, each data object of type *int* occupies 4 bytes of memory no matter what the value of the variable is. In other words, a small integer of value 23 and a large integer of value 4,294,967,294 both occupy 4 bytes of memory or 32 bits of binary data.

> Data in memory are stored in binary form.

**Storage of Data in Sources or Sinks** Sources and sinks of data also store data in a chunk of bytes, but data can be either binary or text. If a data item is stored as binary, the type of the data defines the number of bytes; if a data item is stored as text, the value of the data defines the number of bytes. For example, the integer 23 can be stored as four bytes (binary) or it can be stored as two characters '2' and '3' (text). The integer 4294967294 can be stored as 4 bytes in binary but 10 bytes in text.

The question is which method of storage we need to use. The following considerations may help us decide.

- The keyboard as a source of data can accept data only as text. Similarly, the monitor as a sink of data shows data only as a set of characters.
- Files as sources or sinks of data can handle both text and binary input/output. The question is how we store data in a file: as binary or as text. If we want to store an object in a file, the format should be binary.
- Strings as sources or sinks of data must be input/output as text; a string is a collection of characters (we discuss this in more detail later in the chapter).

**Storage of Data in Buffer of Streams** Streams deliver data to a sink or receive data from a source in bulk. This means the stream buffer should exactly match the sink or source it is connected to. In other words, if the source or sink is using text data, the stream must use text data; if the source or sink is using binary data, the source or the sink must use binary data. As we will see later, the streams are designed to operate in text mode by default; if we want them to operate in binary mode, the stream object must be instantiated as binary. A question: If memory operates in binary and the stream operates in text or binary (based on the source or sink it is connected to), how is this disparity resolved? This is one of the main purposes of using streams. A stream always accepts data or delivers data to memory in binary, but it converts the data as necessary to match the need of the source or sink. Figure 16.4 shows this responsibility.

**Note:** The stream is responsible for changing data from text to binary and vice versa.

![](img/d68f6199646ca63591a6d8419e0ed4ba_737_0.png)

**Figure 16.4** Responsibility of streams

### 16.6.1 Stream Classes

To handle input/output operations, the C++ library defines a hierarchy of classes (Figure 16.5).

### The ios Class

At the top of the hierarchy is the *ios* class, which serves as a virtual base class. The *ios* class is the base class for all input/output classes. It defines data members and member functions that are inherited by all input/output stream classes. Since the *ios* class is never instantiated, it does not use its data members and member functions. They are used by other stream classes.

> **The ios class cannot be instantiated.**

![](img/d68f6199646ca63591a6d8419e0ed4ba_737_1.png)

**Figure 16.5** Basic stream hierarchy in C++

**Table 16.1** Five steps in using a stream

| | |
|---|---|
| 1. | Construct the stream |
| 2. | Connect the stream to the source or sink |
| 3. | Read or write from the stream |
| 4. | Disconnect the source or the sink |
| 5. | Destroy the stream |

### Other Classes

For convenience, we refer to *istream*, *ostream*, and *iostream* as console classes (they are used to connect our program to the console); we refer to *ifstream*, *ofstream*, and *fstream* as file streams (they are used to connect our program to files); and we refer to *istringstream*, *ostringstream*, and *stringstream* as string streams.

### Using Streams

To use any streams, we must consider the chain of five actions shown in Table 16.1. An appropriate stream object is constructed, the object is connected to the source or sink, data are read from the source or written to the sink, the source or sink is disconnected from the stream, and the stream is destroyed.

### Characteristics of Stream Objects

When we work with stream objects, we need to know that none of the classes in the hierarchy have provided a copy constructor or assignment operators. We should also know that the objects of these classes will change when they are used. This means that we should remember three facts about the objects instantiated from these classes:

- We can never pass an object of any stream class to a function by value (doing so requires a copy constructor). Passing these objects must be by reference.
- We can never return an object of any stream class from a function by value (doing so requires a copy constructor); returning must be done by reference.
- We cannot pass or return an object of any stream class using a constant modifier; the nature of these objects requires change.

## 16.2 CONSOLE STREAMS

In this section we discuss the **console streams**: *istream*, *ostream*, and *iostream*. We can use the first two, but the *iostream* class cannot be instantiated. It is defined as a superclass for other classes in the hierarchy, as we will see later in the chapter.

### 16.2.1 Console Objects

We first discuss the objects created from the two console stream classes.

### The istream Object: cin

The *istream* class defines a class that allows us to read data from the keyboard into our program. We cannot instantiate this class. However, the system has created an object of this class, named *cin*, which is stored in the `<iostream>` header file. The system also connects the *cin* object to the keyboard as shown in Figure 16.6.

![](img/d68f6199646ca63591a6d8419e0ed4ba_739_0.png)

When our program goes out of scope, the `cin` object is destroyed and is automatically disconnected from the keyboard. This means that four out of five tasks, as defined in Table 16.1, are automatically done for us by the system; we simply use the member functions defined in this class to read data from the keyboard.

> **The system has created an object from stream class, named `cin`, and stored it in the `<iostream>` header.**

### The ostream Objects: `cout`, `cerr`, and `clog`

The *ostream* class defines a class that allows us to write data from our program to the monitor. We cannot instantiate this class. However, the system has created three objects of this class (named *cout*, *cerr*, and *clog*) that are stored in the `<iostream>` header file. The system also connects all three objects to the monitor. When our program goes out of scope, these objects are automatically destroyed and are automatically disconnected from the monitor. This means that four out of five tasks, as defined in Table 16.1, are automatically done for us by the system. We can only use the member functions defined in this class to write data to the monitor. Figure 16.7 shows the connection of these objects to the monitor and our program.

There are important points about these objects. First, *cout* is tied to the *cin* object, which means every time we want to input data through the *cin* object, the *cout* object is flushed (emptied). Second, both *cerr* and *clog* are designed to send errors to the console. The difference is that the *cerr* object flushes its contents immediately after each operation; the *clog* object collects the error messages and is flushed whenever the program terminates or when it is explicitly flushed.

![](img/d68f6199646ca63591a6d8419e0ed4ba_739_1.png)
