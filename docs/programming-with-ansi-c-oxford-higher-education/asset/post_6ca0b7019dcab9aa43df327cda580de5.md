
## Brief Contents

Preface to the Second Edition v

Preface to the First Edition viii

Features of the Book x

- 1. Object-oriented Programming and C++ 1
- 2. Overview of the C++ Language 39
- 3. Classes and Objects 69
- 4. Functions 109
- 5. Constructors and Destructors 175
- 6. Operator Overloading and User-defined Conversions 227
- 7. Templates 279
- 8. Exception Handling 328
- 9. Inheritance 362
- 10. Run-time Polymorphism by Virtual Functions 403
- 11. Run-time Type Information and Casting Operators 438
- 12. Streams and Formatted Input/Output 470
- 13. Using Files for Input/Output 497
- 14. Namespaces 525
- 15. String Objects 545
- 16. Standard Template Library 555

Appendix: Case Study 593

Index 617

## 3. CLASSES AND OBJECTS 69

- 3.1 Introduction to Class and Object 69
- 3.2 Classes and Their Attributes 71
- 3.3 Anatomy of Class 71
- 3.4 Access Specifiers 74
- 3.4.1 Expression Parser 75
- 3.5 Storage Requirements 78
- 3.6 Difference between Structure and Class in C++ 80
- 3.7 Difference between Unions and Classes 82
- 3.8 Defining Function Members Outside Class 84
- 3.9 Static Data Members 85
- 3.10 Arrays of Objects 94
- 3.11 Pointer to Objects and Pointer to Members of a Class 95
- 3.12 Nested Classes 98
- 3.13 Local Classes 101
- 3.14 Assigning Objects 103
- 3.15 Constant Objects 104

## 4. FUNCTIONS 109

- 4.1 Introduction 109
- 4.2 Similarities with C Functions 109
- 4.3 main() in C++ 111
- 4.4 Inline Functions 111
- 4.5 Default Arguments 115
- 4.5.1 Using Static Variable as Default Argument to a Function 118
- 4.5.2 Functions with Objects as Parameters 119
- 4.5.3 NRV Optimization 122
- 4.6 Call by Reference 124
- 4.7 Returning a Reference 126
- 4.8 Prototyping and Overloading 132
- 4.8.1 Prototyping 133
- 4.8.2 Function Overloading 133
- 4.9 Program Readability and Default Arguments 136
- 4.10 Member and Non-member Functions 136
- 4.10.1 Deciding to Make a Function a Member or a Non-member 139
- 4.11 Friend Functions 140
- 4.11.1 Need for Friend Functions 143
- 4.12 const and volatile Functions 148
- 4.12.1 const Functions 148
- 4.12.2 Mutable Data Members 148
- 4.12.3 volatile Functions 149
- 4.13 Static Functions 149
- 4.13.1 Restrictions on Static Function 151
- 4.14 Private and Public Functions 152
- 4.15 Functions that Return Objects 154
- 4.16 Function Pointers 157
- 4.17 Using Pointer to Member Function 160
- 4.18 Linkage Specification 169

## 5. CONSTRUCTORS AND DESTRUCTORS 175

- 5.1 Similar-to-built-in Behaviour Concept 175
- 5.2 Need for Object Initialization 175
- 5.3 Introduction to Constructors 177
- 5.4 Rules for Defining Constructors 178
- 5.5 Default Constructors 179
- 5.5.1 Compiler-defined Default Constructor 179
- 5.5.2 User-defined Default Constructor 180
- 5.6 Constructors with One Parameter 185
- 5.7 Explicit Constructors 187
- 5.8 Parameterized Constructors 188
- 5.9 Multiple Constructors 190
- 5.9.1 Constructors with Default Arguments 192
- 5.9.2 Dynamic Initialization and Assignment Operator 194

- 2.9.1 Scope Resolution Operator 59
- 2.9.2 new and delete Operators 60
- 2.9.3 Placement new 63
- 2.9.4 new vs malloc() 64
- 2.9.5 Significance of delete Operator 65
- 2.9.6 New Casting Operators, typeid, and throw 65
- 2.10 Conditional Structures and Looping Constructs 66

7.2.12 Overloading a Template 296
7.2.13 Overloading One Generic Function with Another 302
7.2.14 Manually Overloaded Functions vs Template Instantiations 303
7.2.15 Default Arguments to Function Templates 303
7.3 Class Templates 304
7.3.1 Defining Functions of Class Templates outside the Class 306
7.3.2 Classes with Multiple Generic Data Types 313
7.3.3 Using Non-type Arguments 314
7.3.4 Using Default Arguments 315
7.3.5 Static Data Members 316
7.3.6 Friends of Class Template 318
7.3.7 Primary and Partial Specialization 319
7.4 Compilation Models for Templates 321
7.4.1 Inline vs Non-inline Function Calls in Multiple Files 321
7.4.2 Template Instantiations in Multiple Files 322
7.5 Use of typename 323
## 8. EXCEPTION HANDLING 328
8.1 Introduction 328
8.2 Traditional Error Handling 328
8.2.1 Returning Error Number 328
8.2.2 Global Flag Manipulation 328
8.2.3 Abnormal Termination of Program 329
8.3 Need for Exception Handling 329
8.3.1 Dividing Error Handling 329
8.3.2 Unconditional Termination 329
8.3.3 Separating Error Reporting and Error Handling 330
8.3.4 Problem of Destroying Objects 330
8.4 Components of Exception Handling Mechanism 330
8.4.1 try Block 330
8.4.2 catch Block 331
8.4.3 throw Expression 331
8.5 Challenges in the New Approach 332
8.5.1 Finding Proper Handlers 332
8.5.2 Finding Proper Handlers for Polymorphic Objects 333
8.5.3 Backtracking until Beginning of try Block 333
8.6 Throwing within and outside Functions 333
8.6.1 Handling Exceptions 338
8.7 Throwing Variables Other than Objects 339
8.8 Using Multiple catch 339
8.9 Catch All 342
8.10 Restricting Exceptions from Functions: Exception Specification 344
8.11 Rethrowing Exceptions 350
8.12 terminate() and unexpected() Functions 353
8.13 uncaught_exception() Function 356
8.14 Exception Handlers and Debuggers 358
8.15 Drawbacks of Exception Handling 358
8.16 Exception Class 359
## 9. INHERITANCE 362
9.1 Introduction 362
9.2 Advantages of using Inheritance 363
9.2.1 Avoiding Creation of Objects from Scratch 363
9.2.2 Avoiding Redundancy and Maintaining Consistency 363
9.2.3 Mapping a Real-world Hierarchy 364
9.3 Is-a and Part of Relationships 364
9.4 Defining Derived Classes 364
9.4.1 Derivation using Public Access Modifier 365
9.4.2 Derivation using Private Access Modifier 366
9.4.3 Protected Access Specifier 368
9.4.4 Derivation using Protected Access Modifier 370
9.5 Inheritance in C++ Object Model 372
9.6 Different Ways to Derive Classes 373
9.6.1 Public Derivation 374

## 10. RUN-TIME POLYMORPHISM BY VIRTUAL FUNCTIONS 403

## 11. RUN-TIME TYPE INFORMATION AND CASTING OPERATORS 438

## 12. STREAMS AND FORMATTED INPUT/OUTPUT 470

- 9.6.2 Private Derivation 374
- 9.6.3 Protected Derivation 374
- 9.6.4 Public and Private Derivation of Protected Access Specifier 375
- 9.7 Access Control 376
- 9.8 Access Declaration 376
- 9.9 Deriving Multiple Classes from a Single Class 378
- 9.10 Multiple Inheritance 381
- 9.10.1 Problems in Multiple Inheritance 383
- 9.11 Deriving a Class from an Already Derived Class 385
- 9.12 Virtual Base Class 387
- 9.13 Applications of Constructors and Destructors 391
- 9.14 Exception Handling in Case of Derivation 391
- 9.15 Composite Objects (Container Objects) 394
- 10.1 Introduction 403
- 10.2 Compile Time and Run-time Polymorphism 404
- 10.3 Pointer to Object 405
- 10.4 this Pointer 405
- 10.5 Compatibility of Derived and Base Class Pointers 406
- 10.5.1 Subobject Concept 408
- 10.6 Base Class and Derived Class Member Functions 408
- 10.7 Virtual Functions 410
- 10.7.1 Static vs Dynamic Binding 415
- 10.7.2 Default Arguments to Virtual Functions 416
- 10.7.3 Advantages of using Virtual Functions 419
- 10.7.4 Virtual Destructors 421
- 10.8 Use of Virtual Functions 422
- 10.9 Pure Virtual Functions 427
- 10.9.1 Static Invocation of Virtual Function 431

- 11.1 Introduction 438
- 11.1.1 Polymorphic Objects 438
- 11.1.2 Need for RTTI 440
- 11.1.3 typeinfo Object and typeid Operator 442
- 11.1.4 Using typeid for Non-polymorphic Objects 443
- 11.1.5 Using typeid for Polymorphic Objects 444
- 11.1.6 Using typeid for Solution 445
- 11.1.7 Applying typeid to Class Names and Objects 448
- 11.1.8 Cases Where RTTI is Useful 448
- 11.1.9 Problems with typeid 449
- 11.2 Dynamic Casting using dynamic_cast 450
- 11.2.1 Using dynamic_cast 451
- 11.2.2 Using dynamic_cast to Replace typeid 453
- 11.2.3 Using dynamic_cast to Solve Problems with typeid 456
- 11.3 Casting using const_cast 459
- 11.4 Casting using static_cast 459
- 11.5 Casting using reinterpret_cast 460
- 11.6 RTTI and Templates 461
- 11.6.1 Using typeid 461
- 11.6.2 Compatibility and Efficiency Issues 464
- 11.7 Cross Casting 464
- 11.8 Downcasting 466
- 12.1 Introduction 470
- 12.2 I/O Streams of C vs C++ 471
- 12.3 Old C++ I/O vs ANSI C++ I/O 472
- 12.4 Predefined and Wide Character Streams 473
- 12.5 C++ Stream Classes Hierarchy 473
- 12.6 Formatted and Unformatted I/O 473
- 12.6.1 put() and get() Functions for cout 474
