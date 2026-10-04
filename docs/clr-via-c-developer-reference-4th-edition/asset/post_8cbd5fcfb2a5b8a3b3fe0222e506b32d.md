
Demystifying Delegates ................................................................................ 396
Using Delegates to Call Back Many Methods (Chaining). ................................ 400
C#s Support for Delegate Chains ................................................................... 404
Having More Control over Delegate Chain Invocation ........................................ 404
Enough with the Delegate Definitions Already (Generic Delegates) ................... 407
C#s Syntactical Sugar for Delegates ................................................................ 408
- Syntactical Shortcut #1: No Need to Construct a Delegate Object. ..................... 409
- Syntactical Shortcut #2: No Need to Define a Callback Method (Lambda Expressions) ............ 410
- Syntactical Shortcut #3: No Need to Wrap Local Variables in Class Manually to Pass Them to a Callback Method 413
Delegates and Reflection ................................................................................... 416

# Chapter 18 Custom Attributes 421
Using Custom Attributes ................................................................................ 421
Defining Your Own Attribute Class ................................................................ 425
Attribute Constructor and Field/Property Data Types ....................................... 428
Detecting the Use of a Custom Attribute ................................................ 430
Matching Two Attribute Instances Against Each Other ....................................... 434
Detecting the Use of a Custom Attribute Without Creating Attribute-Derived Objects 437
Conditional Attribute Classes ................................................................ 440

# Chapter 19 Nullable Value Types 441
C#s Support for Nullable Value Types ................................................ 443
C#s Null-Coalescing Operator ............................................................ 446
The CLR Has Special Support for Nullable Value Types ........................ 447
- Boxing Nullable Value Types ................................................... 447
- Unboxing Nullable Value Types ............................................... 448
- Calling GetType via a Nullable Value Type ................................... 448
- Calling Interface Methods via a Nullable Value Type ................ 448

# Chapter 20 Exceptions and State Management 451
Defining "Exception" ............................................ 452
Exception-Handling Mechanics ...................................... 453
The try Block...................................................... 454
The catch Block..................................................... 455
The finally Block................................................... 456
The System.Exception Class......................................... 460
FCL-Defined Exception Classes...................................... 463
Throwing an Exception .............................................. 466
Defining Your Own Exception Class.................................. 467
Trading Reliability for Productivity ............................... 469
Guidelines and Best Practices....................................... 478
Use finally Blocks Liberally ....................................... 478
Don't Catch Everything ............................................. 480
Recovering Gracefully from an Exception ............................ 481
Backing Out of a Partially Completed Operation When an Unrecoverable Exception Occurs—Maintaining State....... 482
Hiding an Implementation Detail to Maintain a "Contract"....... 483
Unhandled Exceptions ............................................... 485
Debugging Exceptions............................................... 490
Exception-Handling Performance ................................ 492
Constrained Execution Regions (CERs) ................................. 494
Code Contracts ................................................. 498

# Chapter 21 The Managed Heap and Garbage Collection 505
Managed Heap ...................................................... 505
Allocating Resources from the Managed Heap ................................. 506
The Garbage Collection Algorithm ................................... 507
Garbage Collections and Debugging ................................ 510
Generations: Improving Performance ................................. 513
Garbage Triggers ........................................... 519
Large Objects ........................................................ 519
Garbage Collection Modes ............................................. 520
Forcing Garbage Collections .......................................... 522
Monitoring Your Application’s Memory Usage ................................. 524
Working with Types Requiring Special Cleanup ................................. 525
Using a Type That Wraps a Native Resource ................................. 532
An Interesting Dependency Issue .................................... 537
Other GC Features for Use with Native Resources ................................. 538
Finalization Internals .............................................. 542
Monitoring and Controlling the Lifetime of Objects Manually ................. 545

# Chapter 22 CLR Hosting and AppDomains 553
CLR Hosting ...................................................... 554
AppDomains ........................................................ 556
Accessing Objects Across AppDomains ................................ 559
AppDomain Unloading ............................................... 570
AppDomain Monitoring .............................................. 571
AppDomain First-Chance Notifications ................................. 573
How Hosts Use AppDomains .......................................... 574
Executable Applications ........................................... 574
Microsoft Silverlight Rich Internet Applications ................................ 574
Microsoft ASP.NET and XML Web Services ......................... 575
Microsoft SQL Server .............................................. 575
Your Own Imagination ............................................. 576
Advanced Host Control ............................................ 576
Managing the CLR by Using Managed Code ........................ 577
Writing a Robust Host Application ............................... 578
How a Host Gets Its Thread Back ................................ 580

# Chapter 23 Assembly Loading and Reflection 584
Assembly Loading ...................................................... 584
Using Reflection to Build a Dynamically Extensible Application .................... 588
Reflection Performance ................................................... 589
Discovering Types Defined in an Assembly ................................... 590
What Exactly Is a Type Object? ................................................................ 591
Building a Hierarchy of Exception-Derived Types ........................ 593
Constructing an Instance of a Type ................................................................ 594
Designing an Application That Supports Add-Ons .......................................... 596
Using Reflection to Discover a Type's Members ................................ 599
Discovering a Type's Members ................................................................. 599
Invoking a Type's Members ................................................................ 603
Using Binding Handles to Reduce Your Process's Memory Consumption ................... 608

# Chapter 24 Runtime Serialization 613
Serialization/Deserialization Quick Start. ....................................... 613
Making a Type Serializable ................................................................ 617
Controlling Serialization and Deserialization ................................................ 619
Formatters Serialize Type Instances ................................................................ 623
Controlling the Serialized/Deserialized Data ................................................ 624
How to Define a Type That ImplementsSerializable When the Base Type Doesn't Implement This Interface ................................. 630
Streaming Contexts ................................................................................ 631
Serialization a Type As a Different Type and Deserializing an Object As a Different Object .......................................... 633
Serialization Surrogates ....................................................................... 636
Surrogate Selector Chains ............................................................... 639
Overriding the Assembly and/or Type When Deserializing an Object ................................................. 640
