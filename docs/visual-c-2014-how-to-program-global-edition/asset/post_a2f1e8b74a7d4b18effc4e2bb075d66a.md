
12.5.1 Creating Abstract Base Class Employee 518

# 16 Contents

12.5.2 Creating Concrete Derived Class SalaryEmployee 520
12.5.3 Creating Concrete Derived Class HourlyEmployee 522
12.5.4 Creating Concrete Derived Class CommissionEmployee 523
12.5.5 Indirect Concrete Derived Class BasePlusClassEmployee 525
12.5.6 Polymorphic Processing, Operator and Downcasting 526
12.5.7 Summary of the Allowed Assignments Between Base-Class and Derived-Class Variables 531
12.6 sealed Methods and Classes 532
12.7 Case Study: Creating and Using Interfaces 533
12.7.1 Developing an IPayable Hierarchy 534
12.7.2 Declaring Interface IPayable 536
12.7.3 Creating Class Invoice 536
12.7.4 Modifying Class Employee to Implement Interface IPayable 538
12.7.5 Using Interface IPayable to Process Invoices and Employees Polymorphically 539
12.7.6 Common Interfaces of the .NET Framework Class Library 541
12.8 Wrap-Up 542

# 13 Exception Handling: A Deeper Look 547

13.1 Introduction 548
13.2 Example: Divide by Zero without Exception Handling 549
13.2.1 Dividing By Zero 550
13.2.2 Enter a Non-Numeric Denominator 551
13.2.3 Unhandled Exceptions Terminate the App 552
13.3 Example: Handling DividingByZeroExceptions and FormatExceptions 552
13.3.1 Encoding Code in a try block 554
13.3.2 Catching Exceptions 554
13.3.3 Caught Exceptions 555
13.3.4 Termination Model of Exception Handling 556
13.3.5 Flow of Control When Exceptions Occur 556
13.4 .NET Exception Hierarchy 557
13.4.1 ClassSystemException 557
13.4.2 Which Exceptions Might a Method? 558
13.5 finally Block 559
13.5.1 Moving Resource-Release Code to a finally Block 559
13.5.2 Demonstrating the Finally Block 560
13.5.3 Throwing Exceptions Using the throw statement 564
13.5.4 Rethrow Exceptions 564
13.5.5 Returning After a finally Block 565
13.6 The using Statement 566
13.7 Exception Properties 567
13.7.1 Property InnerException 567
13.7.2 Other Exception Properties 568
13.7.3 Demonstrating Exception Properties and Stack Unwinding 568
13.7.4 Throwing an Exception with an InnerException 570
13.7.5 Displaying Information About the Exception 571
13.8 User-Defined Exception Classes 571
13.9 Checking for null? References: Introducing C# 6.0 Operator 575
13.9.1 Null-Conditional Operator (?) 575
13.9.2 Revisiting Operators is not 576
13.9.3 Nullable Types 576
13.9.4 Null Coalescing Operator (??) 577
13.10 Exception Filters and the C# 6.0 when Clause 577
13.11 Wrap-Up 578

# 14 Graphical User Interfaces with Windows Forms: Part I 584

14.1 Introduction 585
14.2 Windows Forms 586
14.3 Event Handling 588
14.3.1 A Simple Event-Driven GUI 589
14.3.2 Auto-Generated GUI Code 591
14.3.3 Delegates and the Event-Handling Mechanism 593
14.3.4 Another Way to Create Event Handlers 594
14.3.5 Locating Event Information 595
14.4 Control Properties and Layout 596
14.4.1 Anchoring and Docking 597
14.4.2 Using Visual Studio to Edit a GUI's Layout 599
14.5 Labels, TextBoxes and Buttons 600
14.6 GroupBoxes and Panels 603
14.7 CheckBoxes and RadioButtons 606
14.7.1 CheckBoxes 606
14.7.2 Combining Font Styles with Bitwise Operators 608
14.7.3 RadioButtons 609
14.8 PictureBoxes 614
14.9 ToolTips 617
14.10 NumericUpDown Control 618
14.11 Mouse-Event Handling 621
14.12 Keyboard-Event Handling 623
14.13 Wrap-Up 627

# 15 Graphical User Interfaces with Windows Forms: Part 2 637

15.1 Introduction 638
15.2 Menus 638
15.3 MonthCalendar Control 648
15.4 DateTimePicker 649
15.5 LinkLabel Control 652
15.6 ListBox Control 655
15.7 CheckedListBox Control 660
15.8 ComboBox Control 663
15.9 TreeView Control 667
15.10 ListView Control 673
15.11 TabControl Control 679
15.12 Multiple Document Interface (MDI) Windows 683
15.13 Visual Inheritance 691
15.14 User-Defined Controls 696
15.15 Wrap-Up 699

# 16 Strings and Characters: A Deeper Look 707

16.1 Introduction 708
16.2 Fundamentals of Characters and Strings 709
16.3 Constructors 710
16.4 Indexer, Length Property and CopyTo Method 711
16.5 Comparing strings 712
16.6 Locating Characters and Substrings 716
16.7 Extracting Substrings from strings 719
16.8 Concatenating strings 720
16.9 Miscellaneous Methods 720
16.10 StringBuilder 722
16.11 Length and Capacity, EnsureCapacity Method and Indexer of StringBuilder 723
16.12 Append and AppendFormat Methods of StringBuilder 725
16.13 Insert, Remove and Replace Methods of StringBuilder 727
16.14 Methods 730
16.15 Introduction to Regular Expressions () 732
16.16 Wrap-Up 732

# 17 Files and Streams 739

17.1 Introduction 740
17.2 Files and Streams 740
17.3 Creating a Sequential-Access File 741
17.4 Reading Data from a Sequential-Access File 750
17.5 Case Study: Injury Program 754
17.6 Serialization 759
17.7 Creating a Sequential-Access File Using Serialization 760
17.8 Reading and Deserializing Data from a Binary File 764
17.9 Classes and Directory 767
17.9.1 Demonstrating Classes and Directory 768
17.9.2 Searching with LINQ 771
17.10 Wrap-Up 775

# 18 Searching and Sorting 783

18.1 Introduction 783
18.2 Searching Algorithms 784
18.2.1 Linear Search 784
18.2.2 Binary Search 788
18.3 Sorting Algorithms 792
18.3.1 Selection Sort 793
18.3.2 Insertion Sort 796
18.3.3 Merge Sort 800
18.4 Summary of the Efficiency of Searching and Sorting 806
18.5 Wrap-Up 807

# 19 Custom Data Structures

19.1 Introduction 813
19.2 Simple-Type structs, Boxing and Unboxing 813
19.3 Self-Referential Classes 814
19.4 Linked Lists 815
19.5 Stacks 828
19.6 Queues 832
19.7 Trees 835
19.7.1 Binary Search Tree of Integer Values 836
19.7.2 Binary Search Tree of IComparable Objects 843
19.8 Wrap-Up 849

# 20 Generics

20.1 Introduction 856
20.2 Motivation for Generic Methods 857
20.3 Generic-Type Implementation 859
20.4 Type Constraints 862
20.4.1 IComparable<T> Interface 862
20.4.2 Specifying Type Constraints 862
20.5 Overloading Generic Methods 865
20.6 Generic Classes 865
20.7 Wrap-Up 875

# 21 Generic Collections; Functional Programming with LINQ/PLINQ

21.1 Introduction 882
21.2 Collections Overview 884
21.3 Class Array and Enumerators 886
21.3.1 C# using static Directive 888
21.3.2 Class UsingArray’s static fields 889
21.3.3 Array Method Sort 889
21.3.4 Array Method Copy 889
21.3.5 Array Method BinarySearch 889
21.3.6 Array Method GetEnumerator and Interface IEnumerator 889
21.3.7 Iterating Over a Collection with foreach 890
21.3.8 Array Methods Clear, IndexOf, LastIndexOf and Reverse 890
21.4 Dictionary Collections 890
21.4.1 Dictionary Fundamentals 891
21.4.2 Using the SortedDictionaryCollection 892
21.5 Generic LinkedList Collection 896
21.6 C# 6 Null Conditional Operator?[] 900
21.7 C# 6 Dictionary Initializers and Collection Initializers 901
21.8 Delegates 901
21.8.1 Declaring a Delegate Type 903
21.8.2 Declaring a Delegate Variable 903
21.8.3 Delegate Parameters 904
21.8.4 Passing a Method Name Directly to the Delegate Parameter 904
21.9 Lambda Expressions 904
21.9.1 Expression Lambdas 906
21.9.2 Assigning Lambdas to Delegate Variables 907
21.9.3 Explicitly Typed Lambda Parameters 907
21.9.4 Statement Lambdas 907
21.10 Introduction to Functional Programming 907
21.11 Functional Programming with LINQ Method-Call Syntax and Lambdas 909
21.11.1 LINQ Extension Methods Min, Max, Sum and Average 912
21.11.2 Aggregate Aggregate Method for Reduction Operations 912
21.11.3 The Where Extension for Filtering Operations 914
21.11.4 Select Extension Method for Mapping Operations 915
21.12 PLNQ: Improving LINQ to Objects Performance for Multicore 915
21.13 (Optional) Covariance and Contravariance for Generic Types 919
21.14 Wrap-Up 921

# 22 Databases and LINQ 933

22.1 Introduction 934
22.2 Relational Databases 935
22.3 A Books Database 936
22.4 LINQ to Entities and the ADO.NET Entity Framework 940
22.5 Querying with LINQ 941
22.5.1 Creating the ADO.NET Entity Data Model Class Library 943
22.5.2 Creating a Windows Forms Project and Configuring It to Use the Data Model 947
22.5.3 Data Bindings Between Controls and the Entity Data Model 949
22.6 Dynamically Binding Query Results 955
22.6.1 Creating the Display Query Results GUI 956
22.6.2 Coding the Display Query Results App 957
22.7 Retrieving Data from Multiple Tables with LINQ 959
