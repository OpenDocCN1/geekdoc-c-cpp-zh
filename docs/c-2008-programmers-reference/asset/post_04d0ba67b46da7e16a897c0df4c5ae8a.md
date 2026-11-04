
## Contents

Introduction XXV

## Part I: C# Fundamentals 1

## Chapter 1: The .NET Framework 3

What's the .NET Framework? 3
Common Language Runtime 3
.NET Framework Class Library 4
Assemblies and the Microsoft Intermediate Language (MSIL) 6
Versions of the .NET Framework and Visual Studio 8
Summary 9

## Chapter 2: Getting Started with Visual Studio 2008 11

Visual Studio 2008 Overview 11
Choosing the Development Settings 12
Resetting the Development Settings 13
Creating a New Project 14
Components of the IDE 17
Code and Text Editor 34
Code Snippets 35
IntelliSense 37
Refactoring Support 39
Debugging 49
Setting Breakpoints 49
Stepping through the Code 51
Watching 52
Autos and Immediate Windows 53
Unit Testing 53
Creating the Test 54
Running the Test 57
Testing with Floating Point Numbers 58
Adding Additional Test Methods 59
Summary 59

## Contents

- Chapter 3: C# Language Foundations 61
- Using Visual Studio 2008 61
- Using the C# Compiler (csc.exe) 64
- Dissecting the Program 66
  - Passing Arguments to Main() 68
- Language Syntax 68
  - Keywords 68
  - Variables 69
  - Scope of Variables 71
  - Constants 74
  - Comments 74
  - XML Documentation 74
- Data Types 78
  - Value Types 79
  - Reference Types 84
  - Enumerations 85
  - Arrays 87
  - Implicit Typing 88
  - Type Conversion 89
- Flow Control 92
  - if-else Statement 92
  - switch Statement 94
- Looping 96
  - for Loop 96
  - Nested for Loop 97
  - foreach 98
  - while and do-while Loops 99
  - Exiting from a Loop 99
  - Skipping an Iteration 102
- Operators 102
  - Assignment Operators 103
  - Relational Operators 105
  - Logical Operators 106
  - Mathematical Operators 108
  - Operator Precedence 109
- Preprocessor Directives 110
  - #define and #undef 111
  - #if, #else, #elif, and #endif 115
  - #warning and #error 117
  - #line 118

#region and #endregion 120
#pragma warning 122
Summary 123

## Chapter 4: Classes and Objects 125

- Classes 125
- Defining a Class 126
- Using Partial Classes 126
- Creating an Instance of a Class (Object Instantiation) 127
- Anonymous Types (C# 3.0) 128
- Class Members 131
- Function Members 134
- Static Classes 156
- System.Object Class 157
- Testing for Equality 158
- Implementing Equals 159
- ToString() Method 161
- Attributes 162
- Structures 165
- Summary 169

## Chapter 5: Interfaces 171

- Defining an Interface 172
- Implementing an Interface 173
- Implementing Multiple Interfaces 174
- Extending Interfaces 175
- Interface Casting 177
- The is and as Operators 178
- Overriding Interface Implementations 179
- Summary 181

## Chapter 6: Inheritance 183

- Understanding Inheritance in C# 183
- Implementation Inheritance 184
- Abstract Class 186
- Abstract Methods 186
- Virtual Methods 189
- Sealed Classes and Methods 191
- Overloading Methods 192

- Using Constraints in a Generic Type 271
- Generic Interfaces 275
- Generic Structs 276
- Generic Methods 276
- Generic Operators 278
- Generic Delegates 280
- **Generics and the .NET Framework Class Library** 280
- **Using the LinkedList<T> Generic Class** 284
- **System.Collections.ObjectModel** 288
- **Summary** 291

## Chapter 10: Threading 293

- **The Need for Multithreading** 293
- Starting a Thread 295
- Aborting a Thread 297
- Passing Parameters to Threads 301
- **Thread Synchronization** 303
- Using Interlocked Class 304
- Using C# Lock 304
- Monitor Class 307
- **Thread Safety in Windows Forms** 312
- Using the BackgroundWorker Control 315
- Testing the Application 320
- **Summary** 320

## Chapter 11: Files and Streams 321

- **Working with Files and Directories** 321
- Working with Directories 322
- Working with Files Using the File and FileInfo Classes 326
- Creating a FileExplorer 329
- **The Stream Class** 331
- BufferedStream 333
- The FileStream Class 334
- MemoryStream 337
- NetworkStream Class 338
- **Cryptography** 343
- Hashing 344
- Salted Hash 346
- Encryption and Decryption 347

## Contents

- **Compressions for Stream Objects** 353
  - Compression 353
  - Decompression 354
- **Serialization** 359
  - Binary Serialization 359
  - XML Serialization 365
- **Summary** 375
- **Chapter 12: Exception Handling** 377
  - **Handling Exceptions** 377
    - Handling Exceptions Using the try-catch Statement 378
    - Handling Multiple Exceptions 381
    - Throwing Exceptions Using the throw Statement 383
    - Rethrowing Exceptions 386
    - Exception Chaining 387
    - Using Exception Objects 389
    - The finally Statement 391
  - **Creating Custom Exceptions** 393
  - **Summary** 395
- **Chapter 13: Arrays and Collections** 397
  - **Arrays** 397
    - Accessing Array Elements 400
    - Multidimensional Arrays 400
    - Arrays of Arrays: Jagged Arrays 402
    - Parameter Arrays 403
    - Copying Arrays 404
  - **Collections Interfaces** 404
    - Dynamic Arrays Using the ArrayList Class 405
    - Indexers and Iterators 407
    - Implementing IEnumerable<T> and IEnumerator<T> 410
    - Implementing Comparison Using IComparer<T> and IComparable<T> 413
    - Dictionary 420
    - Stacks 422
    - Queues 423
  - **Summary** 424

## Chapter 14: Language Integrated Query (LINQ) 425

### LINQ Architecture 425

### LINQ to Objects 426

- Query Syntax versus Method Syntax and Lambda Expressions 429
- LINQ and Extension Methods 430
- LINQ and Anonymous Types 436

### LINQ to DataSet 438

- Reshaping Data 441
- Aggregate Functions 442
- Joining Tables 443
- Typed DataSet 446
- Detecting Null Fields 449
- Saving the Result of a Query to a DataTable 449

### LINQ to XML 450

- Creating XML Trees 450
- Querying Elements 452
- An Example Using RSS 453

### LINQ to SQL 458

- Using the Object Relational Designer 458
- Querying 460
- Inserting New Rows 461
- Updating Rows 463
- Deleting Rows 463

### Summary 465

## Chapter 15: Assemblies and Versioning 467

### Assemblies 467

- Structure of an Assembly 467
- Examining the Content of an Assembly 468
- Single and Multi-File Assemblies 469
- Understanding Namespaces and Assemblies 480

### Private versus Shared Assemblies 486

- Creating a Shared Assembly 488
- The Global Assembly Cache 492
- Putting the Shared Assembly into GAC 493
- Making the Shared Assembly Visible in Visual Studio 495
- Using the Shared Assembly 496

### Summary 499

## Contents

## Part II: Application Development Using C# 501

## Chapter 16: Developing Windows Applications 503

- The Project 503
  - Configuring the FTP Server 504
  - Creating the Application 506
  - Using Application Settings 508
  - Coding the Application 513
  - Building the Directory Tree and Displaying Images 515
  - Creating a New Directory 522
  - Removing a Directory 523
  - Uploading Photos 524
  - Deleting a Photo 525
  - Testing the Application 526
- Adding Print Capability 526
  - Basics of Printing in .NET 526
  - Adding Print Support to the Project 527
- Deploying the Application 533
  - Publishing the Application Using ClickOnce 534
  - Updating the Application 536
  - Programmatically Updating the Application 538
  - Rolling Back 541
  - Under the Hood: Application and Deployment Manifests 541
- Summary 543

## Chapter 17: Developing ASP.NET Web Applications 545

- About ASP.NET 545
  - How ASP.NET Works 546
  - What Do You Need to Run ASP.NET? 546
- Data Binding 547
  - Modeling Databases Using LINQ to SQL 548
  - Data Binding Using the GridView Control 549
  - Displaying Publisher's Name 554
  - Displaying Titles from a Selected Publisher 555
  - Making the Publisher Field Editable 559
- Building Responsive Applications Using AJAX 560
  - AJAX Control Toolkit 561
  - AJAX-Enabling a Page Using the ScriptManager Control 563
  - Using the UpdatePanel Control 563
  - Using Triggers to Cause an Update 564
