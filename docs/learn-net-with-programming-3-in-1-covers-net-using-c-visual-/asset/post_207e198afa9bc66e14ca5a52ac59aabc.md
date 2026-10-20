
have their own implementation of an animal sound (the pig oinks, and the cat meows, etc.):

# Example:

```
Class Animal // Base class (parent)
{
	Public void animalsound()
	{
		Console.writeline("The animal makes a sound");
	}
}

Class Pig : Animal // Derived class (child)
{
	Public void animalsound()
	{
		Console.writeline("The pig says: wee wee");
	}
}

Class Dog : Animal // Derived class (child)
```

```
Public void animalsound()
{
    Console.writeline("The dog says: bow wow");
}
}
```

## 2.25 Abstract Classes and Methods

Data abstraction is the process of hiding certain details and showing only essential information to the user.

Abstraction can be achieved with either abstract classes or interfaces (which you will learn more about in the next chapter).

The abstract keyword is used for classes and methods:

- Abstract class: is a restricted class that cannot be used to create objects (to access it, it must be inherited from another class).
- Abstract method: can only be used in an abstract class, and it does not have a body. The body is provided by the derived class (inherited from).

An abstract class can have both abstract and regular methods:

```
// Abstract class
```

```
Abstract class Animal
```

```
{
// Abstract method (does not have a body)
Public abstract void animal Sound();
 // Regular method
Public void sleep()
{
	Console.writeline("Zzz");
}
}
// Derived class (inherit from Animal)
Class Pig : Animal
{
	Public override void animalSound()
	{
		// The body of animalSound() is provided here
		Console.writeline("The pig says: wee wee");
	}
}
}
```

```
```csharp
Class Program
{
	Static void Main(string[] args)
	{
		Pig mypig = new Pig(); // Create a Pig object
		MyPig.animalsound(); // Call the abstract method
		MyPig.sleep(); // Call the regular method
	}
}
```
```

## 2.26 Interfaces

Another way to achieve abstraction in C#, is with interfaces. An interface is a completely "abstract class", which can only contain abstract methods and properties (with empty bodies):

Example:

```
```csharp
// interface
Interface Animal
{
	Void animalsound(); // interface method (does not have a body)
}
```
```

```
Void run(); // interface method (does not have a body)
}
```

### Multiple Interfaces

To implement multiple interfaces, separate them with a comma:

Example:

```
Interface ifirstinterface
{
Void mymethod(); // interface method
}
```

```
Interface isecondinterface
{
Void myotherm method(); // interface method
}
```

```
// Implement multiple interfaces
Class democlass : ifirstinterface, isecondinterface
{
Public void mymethod()
{
```

```
Console.writeline("Some text..");
}
Public void myothermethod()
{
    Console.writeline("Some other text...");
}
}
Class Program
{
    Static void Main(string[] args)
    {
        Democlass myobj = new democlass();
        Myobj.mymethod();
        Myobj.myothermethod();
    }
}
```

# C# Enums

An enum is a special "class" that represents a group of constants (unchangeable/read-only variables).To create

an enum, use the enum keyword (instead of class or interface), and separate the enum items with a comma:

Example:

```
Enum Level
{
  Low,
  Medium,
  High
}
```

Enum inside a Class

You can also have an enum inside a class:

Example:

```
Class Program
{
  Enum Level
  {
    Low,
    Medium,
    High
```

```
}
Static void Main(string[] args)
{
    Level myvar = Level.Medium;
    Console.writeline(myvar);
}
}
```

The output will be:

Medium

# CHAPTER 3

# C# LIBRARIES AND .NET ADVANCE FEATURES

## 3.1 Input output (Streams Classes)

# C# - Stream

C# includes following standard IO (Input/Output) classes to read/write from different sources like files, memory, network, isolated storage, etc.

**Stream:** System.IO.Stream is an abstract class that provides standard methods to transfer bytes (read, write, etc.) To the source. It is like a wrapper class to transfer bytes. Classes that need to read/write bytes from a particular source must implement the Stream class. The following classes inherit Stream class to provide the functionality to Read/Write bytes from a particular source:

**Filestream:** Reads or writes bytes from/to a physical file, whether it is a .txt, .exe, .jpg, or any other file. Filestream is derived from the Stream class.

** Memorystream:** memorystream reads or writes bytes that are stored in memory.

**Bufferedstream:** bufferedstream reads or writes bytes from other Streams to improve certain I/O operations' performance.

**Networkstream:** networkstream reads or writes bytes from a network socket.

**Pipestream:** pipestream reads or writes bytes from different processes.

**Cryptostream:** cryptostream is for linking data streams to cryptographic transformations. The following diagram shows the hierarchy of stream classes:

![](img/e7ca4af023a4148a909dd82c11f81893_119_0.png)

Figure 3.1 Stream Classes Hierarchy

# Stream Readers and Writers

**Streamreader:** streamreader is a helper class for reading characters from a Stream by converting bytes into characters using an encoded value. It can be used to

read strings (characters) from different Streams like filestream, memorystream, etc.

**Streamwriter:** streamwriter is a helper class for writing a string to a Stream by converting characters into bytes. It can be used to write strings to different Streams such as as filestream, memorystream, etc.

**Binaryreader:** binaryreader is a helper class for reading primitive datatype from bytes.

**Binarywriter:** binarywriter writes primitive types in binary.

![](img/e7ca4af023a4148a909dd82c11f81893_120_0.png)

Figure 3.2 Stream IO

The above image shows that filestream reads bytes from a physical file, and then streamreader reads strings by converting those bytes to strings. In the same way, the streamwriter takes a string and converts it into bytes and writes to the filestream, and then the filestream writes the bytes to a physical file. So, the filestream deals with bytes, where as streamreader and streamwriter deals with strings.

## 3.2 C# - Multithreading

A thread is defined as the execution path of a program. Each thread defines a unique flow of control. If your application involves complicated and time consuming operations, then it is often helpful to set different execution paths or threads, with each thread performing a particular job.

Threads are lightweight processes. One common Example: of use of thread is implementation of concurrent programming by modern operating systems. Use of threads saves wastage of CPU cycle and increase efficiency of an application.

So far we wrote the programs where a single thread runs as a single process which is the running instance of the application. However, this way the application can perform one job at a time. To make it execute more than one task at a time, it could be divided into smaller threads.

## 3.3 Thread Life Cycle

The life cycle of a thread starts when an object of the System.Threading.Thread class is created and ends when the thread is terminated or completes execution.

Following are the various states in the life cycle of a thread:

**The Unstarted State** – It is the situation when the instance of the thread is created but the Start method is not called.

**The Ready State** – It is the situation when the thread is ready to run and waiting CPU cycle.

**The Not Runnable State** – A thread is not executable, when:

- Sleep method has been called
- Wait method has been called
- Blocked by I/O operations

**The Dead State** – It is the situation when the thread completes execution or is aborted.

# **The Main Thread**

In C#, the System.Threading.Thread class is used for working with threads. It allows creating and accessing individual threads in a multithreaded application. The first thread to be executed in a process is called the main thread.

When a C# program starts execution, the main thread is automatically created. The threads created using the Thread class are called the child threads of the main thread. You can access a thread using the currentThread property of the Thread class.

The following program demonstrates main thread execution –
