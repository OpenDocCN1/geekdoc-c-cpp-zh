
- 10.3.4 Rules and Restrictions on Operator Overloading 454

### 10.4 Overloading Binary Operators 455
### 10.5 Overloading the Binary Stream Insertion and Stream Extraction Operators 455
### 10.6 Overloading Unary Operators 459
### 10.7 Overloading the Increment and Decrement Operators 460
### 10.8 Case Study: A `Date` Class 461
### 10.9 Dynamic Memory Management 466
### 10.10 Case Study: `Array` Class 468
- 10.10.1 Using the `Array` Class 469
- 10.10.2 `Array` Class Definition 473
### 10.11 Operators as Member vs. Non-Member Functions 480
### 10.12 Converting Between Types 481
### 10.13 `explicit` Constructors and Conversion Operators 482
### 10.14 Overloading the Function Call Operator `()` 485
### 10.15 Wrap-Up 485

## 11 Object-Oriented Programming: Inheritance 497
### 11.1 Introduction 498
### 11.2 Base Classes and Derived Classes 499
- 11.2.1 `CommunityMember` Class Hierarchy 499
- 11.2.2 Shape Class Hierarchy 500
### 11.3 Relationship between Base and Derived Classes 501
- 11.3.1 Creating and Using a `CommissionEmployee` Class 501
- 11.3.2 Creating a `BasePlusCommissionEmployee` Class Without Using Inheritance 506
- 11.3.3 Creating a `CommissionEmployee`–`BasePlusCommissionEmployee` Inheritance Hierarchy 511
- 11.3.4 `CommissionEmployee`–`BasePlusCommissionEmployee` Inheritance Hierarchy Using `protected` Data 515
- 11.3.5 `CommissionEmployee`–`BasePlusCommissionEmployee` Inheritance Hierarchy Using `private` Data 519
### 11.4 Constructors and Destructors in Derived Classes 523
### 11.5 `public`, `protected` and `private` Inheritance 525
### 11.6 Wrap-Up 526

## 12 Object-Oriented Programming: Polymorphism 531
### 12.1 Introduction 532
### 12.2 Introduction to Polymorphism: Polymorphic Video Game 533
### 12.3 Relationships Among Objects in an Inheritance Hierarchy 534
- 12.3.1 Invoking Base-Class Functions from Derived-Class Objects 534
- 12.3.2 Aiming Derived-Class Pointers at Base-Class Objects 537
- 12.3.3 Derived-Class Member-Function Calls via Base-Class Pointers 538
### 12.4 Virtual Functions and Virtual Destructors 540
- 12.4.1 Why `virtual` Functions Are Useful 540
- 12.4.2 Declaring `virtual` Functions 540
- 12.4.3 Invoking a `virtual` Function Through a Base-Class Pointer or Reference 541
- 12.4.4 Invoking a `virtual` Function Through an Object’s Name 541
- 12.4.5 `virtual` Functions in the CommissionEmployee Hierarchy 541
- 12.4.6 `virtual` Destructors 546
- 12.4.7 C++11: `final` Member Functions and Classes 546
### 12.5 Type Fields and `switch` Statements 547
### 12.6 Abstract Classes and Pure `virtual` Functions 547
- 12.6.1 Pure `virtual` Functions 548
- 12.6.2 Device Drivers: Polymorphism in Operating Systems 549
### 12.7 Case Study: Payroll System Using Polymorphism 549
- 12.7.1 Creating Abstract Base Class `Employee` 550
- 12.7.2 Creating Concrete Derived Class `SalariedEmployee` 553
- 12.7.3 Creating Concrete Derived Class `CommissionEmployee` 556
- 12.7.4 Creating Indirect Concrete Derived Class `BasePlusCommissionEmployee` 558
- 12.7.5 Demonstrating Polymorphic Processing 560
### 12.8 (Optional) Polymorphism, Virtual Functions and Dynamic Binding “Under the Hood” 563
### 12.9 Case Study: Payroll System Using Polymorphism and Runtime Type Information with Downcasting, `dynamic_cast`, `typeid` and `type_info` 567
### 12.10 Wrap-Up 570

## 13 Stream Input/Output: A Deeper Look 577
### 13.1 Introduction 578
### 13.2 Streams 579
- 13.2.1 Classic Streams vs. Standard Streams 579
- 13.2.2 `iostream` Library Headers 580
- 13.2.3 Stream Input/Output Classes and Objects 580
### 13.3 Stream Output 581
- 13.3.1 Output of `char*` Variables 581
- 13.3.2 Character Output Using Member Function `put` 582
### 13.4 Stream Input 582
- 13.4.1 `get` and `getline` Member Functions 583
- 13.4.2 `istream` Member Functions `peek`, `putback` and `ignore` 586
- 13.4.3 Type-Safe I/O 586
### 13.5 Unformatted I/O Using `read`, `write` and `gcount` 586
### 13.6 Stream Manipulators: A Deeper Look 587
- 13.6.1 Integral Stream Base: `dec`, `oct`, `hex` and `setbase` 588
- 13.6.2 Floating-Point Precision (`precision`, `setprecision`) 588
- 13.6.3 Field Width (`width`, `setw`) 590
- 13.6.4 User-Defined Output Stream Manipulators 591
### 13.7 Stream Format States and Stream Manipulators 592
- 13.7.1 Trailing Zeros and Decimal Points (`showpoint`) 593
- 13.7.2 Justification (`left`, `right` and `internal`) 594
- 13.7.3 Padding (`fill`, `setfill`) 595
- 13.7.4 Integral Stream Base (`dec`, `oct`, `hex`, `showbase`) 597
- 13.7.5 Floating-Point Numbers; Scientific and Fixed Notation (`scientific`, `fixed`) 597
- 13.7.6 Uppercase/Lowercase Control (`uppercase`) 598
- 13.7.7 Specifying Boolean Format (`boolalpha`) 599
- 13.7.8 Setting and Resetting the Format State via Member Function `flags` 600
### 13.8 Stream Error States 601
### 13.9 Tying an Output Stream to an Input Stream 604
### 13.10 Wrap-Up 605

## 14 File Processing 615
### 14.1 Introduction 616
### 14.2 Files and Streams 616
### 14.3 Creating a Sequential File 617
- 14.3.1 Opening a File 618
- 14.3.2 Opening a File via the `open` Member Function 619
- 14.3.3 Testing Whether a File Was Opened Successfully 619
- 14.3.4 Overloaded `bool` Operator 620
- 14.3.5 Processing Data 620
- 14.3.6 Closing a File 620
- 14.3.7 Sample Execution 621
### 14.4 Reading Data from a Sequential File 621
- 14.4.1 Opening a File for Input 622
- 14.4.2 Reading from the File 622
- 14.4.3 File-Position Pointers 622
- 14.4.4 Case Study: Credit Inquiry Program 623
### 14.5 C++14: Reading and Writing Quoted Text 626
### 14.6 Updating Sequential Files 627
### 14.7 Random-Access Files 628
### 14.8 Creating a Random-Access File 629
- 14.8.1 Writing Bytes with `ofstream` Member Function `write` 629
- 14.8.2 Converting Between Pointer Types with the `reinterpret_cast` Operator 629
- 14.8.3 Credit-Processing Program 630
- 14.8.4 Opening a File for Output in Binary Mode 633
### 14.9 Writing Data Randomly to a Random-Access File 633
- 14.9.1 Opening a File for Input and Output in Binary Mode 635
- 14.9.2 Positioning the File-Position Pointer 635
### 14.10 Reading from a Random-Access File Sequentially 635
### 14.11 Case Study: A Transaction-Processing Program 637
### 14.12 Object Serialization 643
### 14.13 Wrap-Up 644

## 15 Standard Library Containers and Iterators 655
### 15.1 Introduction 656
### 15.2 Introduction to Containers 658
### 15.3 Introduction to Iterators 662
### 15.4 Introduction to Algorithms 667
### 15.5 Sequence Containers 667
- 15.5.1 `vector` Sequence Container 668
- 15.5.2 `list` Sequence Container 675
- 15.5.3 `deque` Sequence Container 680
### 15.6 Associative Containers 681
- 15.6.1 `multiset` Associative Container 682
- 15.6.2 `set` Associative Container 685
- 15.6.3 `multimap` Associative Container 687
- 15.6.4 `map` Associative Container 689
### 15.7 Container Adapters 690
- 15.7.1 `stack` Adapter 691
- 15.7.2 `queue` Adapter 693
- 15.7.3 `priority_queue` Adapter 694
### 15.8 Class `bitset` 695
### 15.9 Wrap-Up 697

## 16 Standard Library Algorithms 707
### 16.1 Introduction 708
### 16.2 Minimum Iterator Requirements 708
### 16.3 Lambda Expressions 710
- 16.3.1 Algorithm `for_each` 711
- 16.3.2 Lambda with an Empty Introducer 711
- 16.3.3 Lambda with a Nonempty Introducer—Capturing Local Variables 712
- 16.3.4 Lambda Return Types 712
### 16.4 Algorithms 712
- 16.4.1 `fill`, `fill_n`, `generate` and `generate_n` 712
- 16.4.2 `equal`, `mismatch` and `lexicographical_compare` 715
- 16.4.3 `remove`, `remove_if`, `remove_copy` and `remove_copy_if` 718
