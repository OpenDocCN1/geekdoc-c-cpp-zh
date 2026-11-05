
```csharp
        }
    }
}

using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using ReflectionDemo;

namespace ConsoleApplication2
{
    class Program
    {
        static void Main(string[] args)
        {
            ApplyReflection.Useme();
        }
    }
}
```

Class    ReflectionDemo.Book
Namespace    ReflectionDemo

Constructors
Void .ctor()
Void .ctor(System.String)

Properties
System.String Title
System.String val

Methods
Method Name    get_Title
Method Name    set_Title
Parameter Type    System.String Parameter Name value
Method Name    Show
Method Name    get_val
Parameter Type    System.String Parameter Name value
Method Name    ToString
Method Name    Equals
Parameter Type    System.Object Parameter Name obj
Method Name    GetHashCode
Method Name    GetType

Input Nil

## Output

|  |
|---|
| Class ReflectionDemo.Book |
| Namespace ReflectionDemo |
| Constructors |
| ReflectionDemo.Book | Book |
| ReflectionDemo.Book | Book |
| Properties |

## Two Marks Questions with Answers

Q.1 What is a Garbage Collector ?

Ans.: Garbage collection is a .Net feature to free the unused code objects in the memory.

The memory heap is divided into three generations. Generation 0, Generation 1 and Generation 2.

Generation 0 - This is used to store short-lived objects. Garbage Collection happens frequently in this Generation.

Generation 1 - This is for medium-lived objects. Usually, the objects that get moved from generation 0 are stored in this.

Generation 2 - This is for long-lived objects.

Collecting a Generation refers to collecting the objects in that generation and all its younger generations. Garbage collection of Generation 2 means full garbage collection, it collects all the objects in Generation 2 as well as Generation 1 and Generation 0.

During the Garbage collection process, as the first phase, the list of live objects is identified. In the second phase, references are updated for those objects which will be compacted. And in the last phase, the space occupied by dead objects are reclaimed. The remaining objects are moved to an older segment.

Q.2 What is the difference between a stack and a heap ?

| Stack | Heap |
|---|---|
| Stored value type | Stored reference type |
| A stack is responsible for keeping track of each executing thread and its location. | The heap is responsible for keeping track of the more precise objects or data. |

Q.3 What are the memory-mapped files ?

Ans.: Memory-mapped files are used to map the content of a file to the logical address of an application. It makes you able to run multiple process on the same machine to share data with each other. To obtain a memory mapped file object, you can use the method MemoryMappedFile.CreateFromFiles( ). It represents a persistent memory-mapped file from a file on disk.

## Q.4 What is the difference between dispose() and finalize() ?

Ans.: Although Dispose and Finalize both methods are used by CLR to perform garbage collection of runtime objects of .NET applications but there is a difference between them.

The Finalize method is called automatically by the runtime while the Dispose method is called by the programmer.

## Q.5 Can multiple catch blocks be executed ?

Ans.: No, Multiple catch blocks can't be executed. Once the proper catch code executed, the control is transferred to the finally block, and then the code that follows the finally block gets executed.

## Q.6 Difference between throw exception and throw clause. AU: May-18

Ans.: Throw clause - In Throw, the original exception stack trace will be retained. To keep the original stack trace information, the correct syntax is 'throw' without specifying an exception.

## Declaration of throw

```csharp
try
{
// do some operation that can fail
}
catch (Exception ex)
{
// do some local cleanup
throw;
}
```

Throw exception - In Throw exception, the original stack trace information will get override and program will lose the original exception stack trace. That is ,'throw ex' resets the stack trace.

```csharp
try
{
// do some operation that can fail
}
catch (Exception ex)
{
    // do some local cleanup
    throw ex;
}
```

So basically the Throw exception overwrites the stack trace and this makes it hard to find the original code line number that has thrown the exception. In turn Throw retains the stack information and adds to the stack information in the exception that it is thrown.

## Long Answered Questions

- Q.1 What are generations in memory management ? (Refer section 13.1)
- Q.2 Discuss GC in .NET environment. (Refer section 13.1)
- Q.3 What are exceptions in C# ? (Refer section 13.2)
- Q.4 What are Pointers in C# ? (Refer section 13.1)
- Q.5 What is the purpose of Reflection ? (Refer section 13.3)
- Q.6 Discuss exception handling in detail. (Refer section 13.2) AU : Dec.-17, May-16
- Q.7 How will you implement security in a site ? Show the different steps. (Refer section 13.3.1) AU : Dec.-17, May-16
- Q.8 Write a C# program to demonstrate IndexOutOfRange Exception. AU : May-18, Marks 6

Ans. :

```csharp
/*
 * C# Program to Demonstrate IndexOutOfRange Exception
 */
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
namespace exceptionsdemo
{
    class arrayoutofindex
    {
        public void calculatedifference()
        {
            int diff=0;
            int [] number= new int[5] {1,2,3,4,5};
            try
            {
                for (int init =1; init <=5; init++)
                {
                    diff = diff - number[init];
                }
                Console.WriteLine("The array difference is:" + diff);
            }
            catch (IndexOutOfRangeException e)
            {
                Console.WriteLine(e.Message);
            }
        }
    }
    class raise_exception
    {
        static void Main(string[] args)
        {
            arrayoutofindex obj = new arrayoutofindex();
            obj.calculatedifference();
            Console.ReadLine();
        }
    }
}
```

Q.9 Explain : Handling exceptions from SQL server. (Refer section 13.2.5)

AU: May-18, Marks 5

Q.10 Explain in detail about attributes. (Refer section 13.3.1)

AU: May-18, Marks 6

Q.11 Write a C# Program to Demonstrate Multiple Exceptions.

AU: Dec.-18, Marks 7

Ans. :

```csharp
/* C# program to demonstrate multiple exception */
namespace ExceptionHandlingDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            int a, b, c;
            Console.WriteLine("ENTER ANY TWO NUMBERS");
            try
            {
                a = int.Parse(Console.ReadLine());
                b = int.Parse(Console.ReadLine());
                c = a / b;
                Console.WriteLine("C VALUE = " + c);
            }
            catch (DivideByZeroException dbze)
            {
                Console.WriteLine("second number should not be zero");
            }
            catch (FormatException fe)
            {
                Console.WriteLine("enter only integer numbers");
            }
            Console.ReadKey();
        }
    }
}
```

**Q.12** Handling exceptions and Returning Exceptions from SQL Server.
*(Refer section 13.2.5)*
**AU : Dec.-18, Marks 6**

**Q.13** Discuss in detail about Reflection.  *(Refer section 13.3.2)*
**AU : Dec.-18, Marks 16**

**Q.14** Explain in detail about Viewing Metadata and Marshalling.
*(Refer section 13.3.2)*
**AU : Dec.-18, Marks 13**

**Q.15** Discuss the commonly used exceptions.
*(Refer section 13.2.3)*
**AU : May-19, Marks 13**

## Notes

## 14.1 Diagnostics and Various Related Tasks

### 14.1.1 Introduction

There are various aspects of software application those need to be monitored and improved over once the application comes in use. In fact, the application can be tested through various angles while it is in development process as well as after its complete development, so that the client does not face any issues. Software application may not always behave as expected. .NET Core provides tools and APIs that helps to diagnose various issues quickly and effectively.

Following are the benefits of Diagnostic tools,

- The ability to monitor performance while debugging.
- Correlate performance data with debugging activity.
- Richer user experience through IntelliTrace and the Output windows.
- Shortening diagnose time to identify and fix an issue.

### 14.1.2 Types of Tools Used for Diagnostic Tasks

- 1. **Debugger Events :** These tools provide access to all Break, Output, and IntelliTrace events during the debugging. The data is presented both as a timeline and as a tabular view. Messages that are sent to the Debug tab of the Output window are captured by IntelliTrace. The post-mortem tools can be used with Windows 7 and later. Windows 8 and later is required to run profiling tools with the debugger (Diagnostic Tools window).
- 2. **The Memory Usage tools :** These tools help developer to monitor the memory usage of the application during debugging. A developer can analyze memory impact, growth, and leak issues simply by looking at the graphs. Code break events allow to identify the parts of the graph that are related to recent debugging activity. Snapshots can be taken before and after debug actions to analyze memory usage and memory growth. Developer can look at the number and size of objects on the heap. .NET Object Allocation tool, helps to identify allocation patterns and anomalies in .NET code.
- 3. **The CPU Usage tools :** These tools track the application's CPU usage while debugging. The CPU Usage tool is a good place to start analyzing application performance. It will tell more about CPU resources that application is consuming. A developer can get a per-function breakdown of CPU usage. To do this go, to Debug > Start Diagnostic Tools without Debugging, select CPU Usage, and click Start.
