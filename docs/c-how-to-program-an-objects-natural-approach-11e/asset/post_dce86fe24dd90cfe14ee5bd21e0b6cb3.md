
### 9.2 Test-Driving an Account Object ........ 433

### 9.3 Account Class with a Data Member and Set and Get Member Functions .... 435

- 9.3.1 Class Definition .................................................. 435
- 9.3.2 Access Specifiers private and public ............................. 437

### 9.4 Account Class: Custom Constructors ...................................... 438

### 9.5 Software Engineering with Set and Get Member Functions .................. 442

### 9.6 Account Class with a Balance ............................................ 444

### 9.7 Time Class Case Study: Separating Interface from Implementation .......... 447

- 9.7.1 Interface of a Class ............................................. 448
- 9.7.2 Separating the Interface from the Implementation .................. 448
- 9.7.3 Class Definition .................................................. 449
- 9.7.4 Member Functions .................................................. 450
- 9.7.5 Including the Class Header in the Source-Code File ................ 450
- 9.7.6 Scope Resolution Operator (::) .................................... 451
- 9.7.7 Member Function setTime and Throwing Exceptions ................... 451
- 9.7.8 Member Functions to24HourString and to12HourString ............... 451
- 9.7.9 Implicitly Inlining Member Functions ............................. 452
- 9.7.10 Member Functions vs. Global Functions ........................... 452
- 9.7.11 Using Class Time ................................................. 452
- 9.7.12 Object Size ...................................................... 454

### 9.8 Compilation and Linking Process ......................................... 454

### 9.9 Class Scope and Accessing Class Members .................................. 455

### 9.10 Access Functions and Utility Functions .................................. 456

### 9.11 Time Class Case Study: Constructors with Default Arguments .............. 457

- 9.11.1 Class Time ....................................................... 457
- 9.11.2 Overloaded Constructors and Delegating Constructors .............. 462

### 9.12 Destructors ............................................................. 463

### 9.13 When Constructors and Destructors Are Called ............................ 464

### 9.14 Time Class Case Study: A Subtle Trap — Returning a Reference or a Pointer to a private Data Member ........ 468

### 9.15 Default Assignment Operator ............................................. 470

### 9.16 const Objects and const Member Functions ................................ 472

### 9.17 Composition: Objects as Members of Classes .............................. 474

### 9.18 friend Functions and friend Classes ..................................... 480

### 9.19 The this Pointer .......................................................... 482

- 9.19.1 Implicitly and Explicitly Using the this Pointer to Access an Object’s Data Members ........ 482
- 9.19.2 Using the this Pointer to Enable Cascaded Function Calls ......... 484

### 9.20 static Class Members: Classwide Data and Member Functions ............... 487

### 9.21 Aggregates in C++20 ....................................................... 492

- 9.21.1 Initializing an Aggregate ........................................ 493
- 9.21.2 C++20 Designated Initializers .................................... 493

### 9.22 Concluding Our Objects Natural Case Study Track: Studying the Vigenère Secret-Key Cipher Implementation ................................ 494

### 9.23 Wrap-Up ................................................................. 507

## 10 OOP: Inheritance and Runtime Polymorphism 529

### 10.1 Introduction ........................................................ 530

### 10.2 Base Classes and Derived Classes ............................ 532

- 10.2.1 CommunityMember Class Hierarchy ..................... 533
- 10.2.2 Shape Class Hierarchy and public Inheritance ....... 534

### 10.3 Relationship Between Base and Derived Classes .......... 535

- 10.3.1 Creating and Using a SalariedEmployee Class ....... 535
- 10.3.2 Creating a SalariedEmployee—SalariedCommissionEmployee Inheritance Hierarchy ........ 538

### 10.4 Constructors and Destructors in Derived Classes .......... 544

### 10.5 Intro to Runtime Polymorphism: Polymorphic Video Game 545

### 10.6 Relationships Among Objects in an Inheritance Hierarchy 546

- 10.6.1 Invoking Base-Class Functions from Derived-Class Objects 547
- 10.6.2 Aiming Derived-Class Pointers at Base-Class Objects 549
- 10.6.3 Derived-Class Member-Function Calls via Base-Class Pointers 550

### 10.7 Virtual Functions and Virtual Destructors ................... 551

- 10.7.1 Why virtual Functions Are Useful ........................ 551
- 10.7.2 Declaring virtual Functions ................................ 552
- 10.7.3 Invoking a virtual Function ................................ 553
- 10.7.4 Virtual Functions in the SalariedEmployee Hierarchy 553
- 10.7.5 virtual Destructors ............................................ 557
- 10.7.6 final Member Functions and Classes ..................... 557

### 10.8 Abstract Classes and Pure virtual Functions ................ 558

- 10.8.1 Pure virtual Functions ......................................... 559
- 10.8.2 Device Drivers: Polymorphism in Operating Systems 559

### 10.9 Case Study: Payroll System Using Runtime Polymorphism 560

- 10.9.1 Creating Abstract Base Class Employee ................ 561
- 10.9.2 Creating Concrete Derived Class SalariedEmployee 563
- 10.9.3 Creating Concrete Derived Class CommissionEmployee 565
- 10.9.4 Demonstrating Runtime Polymorphic Processing ..... 567

### 10.10 Runtime Polymorphism, Virtual Functions and Dynamic Binding “Under the Hood” ....................................................... 570

### 10.11 Program to an Interface, Not an Implementation ........ 573

- 10.11.1 Rethinking the Employee Hierarchy—CompensationModel Interface ............................. 575
- 10.11.2 Class Employee .................................................. 575
- 10.11.3 CompensationModel Implementations .................. 577
- 10.11.4 Testing the New Hierarchy .................................. 579
- 10.11.5 Dependency Injection Design Benefits .................. 580

### 10.12 Wrap-Up ................................................................. 581

## 11 Operator Overloading, Copy/Move Semantics and Smart Pointers 587

### 11.1 Introduction ........................................................ 588

### 11.2 Using the Overloaded Operators of Standard Library Class string 590

### 11.3 Operator Overloading Fundamentals ........................................ 596

- 11.3.1 Operator Overloading Is Not Automatic ............................... 596
- 11.3.2 Operators That Cannot Be Overloaded ................................. 596
- 11.3.3 Operators That You Do Not Have to Overload ......................... 596
- 11.3.4 Rules and Restrictions on Operator Overloading ..................... 597

### 11.4 (Downplaying) Dynamic Memory Management with new and delete .............. 598

### 11.5 Modern C++ Dynamic Memory Management: RAII and Smart Pointers ............ 600

- 11.5.1 Smart Pointers ...................................................... 601
- 11.5.2 Demonstrating unique_ptr ........................................... 601
- 11.5.3 unique_ptr Ownership ................................................ 603
- 11.5.4 unique_ptr to a Built-In Array ...................................... 603

### 11.6 MyArray Case Study: Crafting a Valuable Class with Operator Overloading .. 604

- 11.6.1 Special Member Functions ............................................ 605
- 11.6.2 Using Class MyArray .................................................. 606
- 11.6.3 MyArray Class Definition ............................................. 615
- 11.6.4 Constructor That Specifies a MyArray’s Size .......................... 617
- 11.6.5 Passing a Braced Initializer to a Constructor ......................... 618
- 11.6.6 Copy Constructor and Copy Assignment Operator ........................ 619
- 11.6.7 Move Constructor and Move Assignment Operator ........................ 622
- 11.6.8 Destructor ........................................................... 626
- 11.6.9 toString and size Functions .......................................... 626
- 11.6.10 Overloading the Equality (==) and Inequality (!=) Operators .......... 627
- 11.6.11 Overloading the Subscript ([]) Operator ............................ 629
- 11.6.12 Overloading the Unary bool Conversion Operator ....................... 630
- 11.6.13 Overloading the Preincrement Operator ............................... 631
- 11.6.14 Overloading the Postincrement Operator .............................. 632
- 11.6.15 Overloading the Addition Assignment Operator (+=) ................... 633
- 11.6.16 Overloading the Binary Stream Extraction (>>) and Stream Insertion (<<) Operators ................................... 633
- 11.6.17 friend Function swap ............................................... 636

### 11.7 C++20 Three-Way Comparison Operator (<=>) ................................ 636

### 11.8 Conversion Between Types .................................................. 640

### 11.9 explicit Constructors and Conversion Operators ........................... 641

### 11.10 Overloading the Function Call Operator () ................................ 644

### 11.11 Wrap-Up ...................................................................... 644

## 12 Exceptions and a Look Forward to Contracts ................................ 653

### 12.1 Introduction ............................................................. 654

### 12.2 Exception-Handling Flow of Control ......................................... 658

- 12.2.1 Defining a Custom Exception Class ................................... 658
- 12.2.2 Demonstrating Exception Handling .................................... 659
- 12.2.3 Enclosing Code in a try Block ........................................ 660
- 12.2.4 Defining a Catch Handler for DivideByZeroException .................. 661
- 12.2.5 Termination Model of Exception Handling .............................. 662
- 12.2.6 Flow of Control When the User Enters a Nonzero Denominator ........... 663
- 12.2.7 Flow of Control When the User Enters a Zero Denominator .............. 663
