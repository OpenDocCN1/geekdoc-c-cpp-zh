+   11.3 Operator Overloading Fundamentals ........................................ 596
+       11.3.1 Operator Overloading Is Not Automatic ............................... 596
+       11.3.2 Operators That Cannot Be Overloaded ................................. 596
+       11.3.3 Operators That You Do Not Have to Overload ......................... 596
+       11.3.4 Rules and Restrictions on Operator Overloading ..................... 597
+   11.4 (Downplaying) Dynamic Memory Management with new and delete .............. 598
+   11.5 Modern C++ Dynamic Memory Management: RAII and Smart Pointers ............ 600
+       11.5.1 Smart Pointers ...................................................... 601
+       11.5.2 Demonstrating unique_ptr ........................................... 601
+       11.5.3 unique_ptr Ownership ................................................ 603
+       11.5.4 unique_ptr to a Built-In Array ...................................... 603
+   11.6 MyArray Case Study: Crafting a Valuable Class with Operator Overloading .. 604
+       11.6.1 Special Member Functions ............................................ 605
+       11.6.2 Using Class MyArray .................................................. 606
+       11.6.3 MyArray Class Definition ............................................. 615
+       11.6.4 Constructor That Specifies a MyArray’s Size .......................... 617
+       11.6.5 Passing a Braced Initializer to a Constructor ......................... 618
+       11.6.6 Copy Constructor and Copy Assignment Operator ........................ 619
+       11.6.7 Move Constructor and Move Assignment Operator ........................ 622
+       11.6.8 Destructor ........................................................... 626
+       11.6.9 toString and size Functions .......................................... 626
+       11.6.10 Overloading the Equality (==) and Inequality (!=) Operators .......... 627
+       11.6.11 Overloading the Subscript ([ ]) Operator ............................ 629
+       11.6.12 Overloading the Unary bool Conversion Operator ....................... 630
+       11.6.13 Overloading the Preincrement Operator ............................... 631
+       11.6.14 Overloading the Postincrement Operator .............................. 632
+       11.6.15 Overloading the Addition Assignment Operator (+=) ................... 633
+       11.6.16 Overloading the Binary Stream Extraction (>>) and
+                Stream Insertion (<<) Operators ................................... 633
+       11.6.17 friend Function swap ............................................... 636
+   11.7 C++20 Three-Way Comparison Operator (<=>) ................................ 636
+   11.8 Conversion Between Types .................................................. 640
+   11.9 explicit Constructors and Conversion Operators ........................... 641
+   11.10 Overloading the Function Call Operator () ................................ 644
+   11.11 Wrap-Up ...................................................................... 644

# 12 Exceptions and a Look Forward to Contracts ................................ 653

+   12.1 Introduction ............................................................. 654
+   12.2 Exception-Handling Flow of Control ......................................... 658
+       12.2.1 Defining a Custom Exception Class ................................... 658
+       12.2.2 Demonstrating Exception Handling .................................... 659
+       12.2.3 Enclosing Code in a try Block ........................................ 660
+       12.2.4 Defining a Catch Handler for DivideByZeroExceptions .................. 661
+       12.2.5 Termination Model of Exception Handling .............................. 662
+       12.2.6 Flow of Control When the User Enters a Nonzero Denominator ........... 663
+       12.2.7 Flow of Control When the User Enters a Zero Denominator .............. 663