

## CHAPTER 6 SOFTWARE DEVELOPMENT WITH TEMPLATES, ITERATORS, AND THE STL

### 6.1 Template Functions 291
- Syntax for a Template Function 293
- Programming Tip: Capitalize the Name of a Template Parameter 293
- Using a Template Function 294
- Pitfall: Failed Unification Errors 294
- A Template Function to Swap Two Values 296
- Programming Tip: Swap, Max, and Min Functions 296
- Parameter Matching for Template Functions 296
- A Template Function to Find the Biggest Item in an Array 297
- Programming Idioms for Template Function Arguments 299
- A Template Function to Search in a Sorted Array 299
- Self-Test Exercises for Section 6.1 301

### 6.2 Template Classes 301
- Syntax for a Template Class 301
- Programming Tip: Use the Class Name Item and the typename Keyword 303
- Pitfall: Do Not Place Using Directives in a Template Implementation 304
- More About the Template Implementation File 304
- Parameter Matching for Member Functions of Template Classes 309
- Using the Template Class 309
- Defining the Story-Writing Program 312
- Self-Test Exercises for Section 6.2 312

### 6.3 The STL's Algorithms 313
- Use of Iterators 313
- STL Algorithm Categories 314
- Iterators for Arrays 316
- Self-Test Exercises for Section 6.3 317

### 6.4 The Node Template Class 317
- Functions That Return a Reference Type 318
- What Happens When a Reference Return Value Is Copied Elsewhere 320
- The Data Member Function Now Requires Two Versions 320
- Header and Implementation Files for the New Node 321
- Self-Test Exercises for Section 6.4 321

### 6.5 An Iterator for Linked Lists 328
- The Node Iterator 328
- The Node Iterator Is Derived from std::iterator 330
- Pitfall: std::iterator Might Not Exist 331
- The Node Iterator's Private Member Variable 331
- Node Iterator—Constructor 331
- Node Iterator—the * Operator 331
- Node Iterator—Two Versions of the ++ Operator 332
- Programming Tip: ++p Is More Efficient Than p++ 334
- Iterators for Constant Collections 334
- Programming Tip: When to Use a Const Iterator 336
- Self-Test Exercises for Section 6.5 336

### 6.6 Linked-List Version of the Bag Template Class with an Iterator 337
- How to Provide an Iterator for a Container Class That You Write 337
- The Bag Iterator 338
- Why the Iterator Is Defined Inside the Bag 339
- Self-Test Exercises for Section 6.6 339
- Chapter Summary and Summary of the Five Bags 347
- Solutions to Self-Test Exercises 348
- Programming Projects 350

## CHAPTER 7 STACKS

### 7.1 The STL Stack Class 353
- The Standard Library Stack Class 354
- Programming Example: Reversing a Word 355
- Self-Test Exercises for Section 7.1 356

### 7.2 Stack Applications 357
- Programming Example: Balanced Parentheses 357
- Programming Example: Evaluating Arithmetic Expressions 359
- Evaluating Arithmetic Expressions—Specification 359
- Evaluating Arithmetic Expressions—Design 360
- Evaluating Arithmetic Expressions—Implementation 366
- Functions Used in the Calculator Program 367
- Evaluating Arithmetic Expressions—Testing and Analysis 367
- Evaluating Arithmetic Expressions—Enhancements 368
- Self-Test Exercises for Section 7.2 368

### 7.3 Implementations of the Stack Class 369
- Array Implementation of a Stack 369
- Linked List Implementation of a Stack 373
- The Koenig Lookup 374
- Self-Test Exercises for Section 7.3 374

### 7.4 More Complex Stack Applications 377
- Evaluating Postfix Expressions 377
- Translating Infix to Postfix Notation 379
- Using Precedence Rules in the Infix Expression 381
- Correctness of the Conversion from Infix to Postfix 383
- Self-Test Exercises for Section 7.4 387
- Chapter Summary 387
- Solutions to Self-Test Exercises 387
- Programming Projects 389

## CHAPTER 8 QUEUES

### 8.1 The STL Queue 394
- The Standard Library Queue Class 395
- Uses for Queues 395
- Self-Test Exercises for Section 8.1 397

### 8.2 Queue Applications 398
- Programming Example: Recognizing Palindromes 398
- Self-Test Exercises for Middle of Section 8.2 400
- Programming Example: Car Wash Simulation 401
- Car Wash Simulation—Specification 401
- Car Wash Simulation—Design 402
- Car Wash Simulation—Implementing the Car Wash Classes 405
- Car Wash Simulation—Implementing the Simulation Function 410
- Self-Test Exercises for End of Section 8.2 411

### 8.3 Implementations of the Queue Class 413
- Array Implementation of a Queue 413
- Programming Tip: Use Small Helper Functions to Improve Clarity 416
- Discussion of the Circular Array Implementation of a Queue 418
- Linked-List Implementation of a Queue 420
- Implementation Details 422
- Programming Tip: Make Note of a "Don't Care" Situations 423
- Pitfall: Which End Is Which 423
- Self-Test Exercises for Section 8.3 426

### 8.4 Implementing the STL Deque Class 426
- Calling the Destructor and Constructor for the Deque's value_type Items 429
- Other Variations on Stacks and Queues 430
- Self-Test Exercises for Section 8.4 430

### 8.5 Reference Return Values for the Stack, Queue, and Other Classes 430
- Chapter Summary 430
- Solutions to Self-Test Exercises 432
- Programming Projects 433

## CHAPTER 9 RECURSIVE THINKING

### 9.1 Recursive Functions 437
- A First Example of Recursive Thinking 437
- Tracing Recursive Calls 439
- Programming Example: An Extension of write_vertical 441
- A Closer Look at Recursion 442
- General Form of a Successful Recursive Function 445
- Self-Test Exercises for Section 9.1 446

### 9.2 Studies of Recursion: Fractals and Mazes 447
- Programming Example: Generating Random Fractals 447
- A Function for Generating Random Fractals—Specification 448
- Design and Implementation of the Fractal Specification 450
- How the Recursion Is Displayed 451
- Programming Example: Traversing a Maze 453
- Traversing a Maze—Specification 453
- Traversing a Maze—Design 455
- Traversing a Maze—Implementation 456
- The Recursive Pattern of Exhaustive Search with Backtracking 458
- Programming Example: The Teddy Bear Game 459
- Pitfall: Forgetting to Use the Return Value from a Recursive Call 459
- Self-Test Exercises for Section 9.2 460

### 9.3 Reasoning About Recursion 461
- How to Ensure That There Is No Infinite Recursion 463
- Inductive Reasoning About the Correctness of a Recursive Function 466
- Self-Test Exercises for Section 9.3 467
- Chapter Summary 468
- Solutions to Self-Test Exercises 468
- Programming Projects 470

## CHAPTER 10 TREES

### 10.1 Introduction to Trees 475
- Binary Trees 475
- Binary Taxonomy Trees 475
- General Trees 479
- Self-Test Exercises for Section 10.1 480

### 10.2 Tree Representations 480
- Array Representation of Complete Binary Trees 480
- Representing a Binary Tree with a Class for Nodes 483
- Self-Test Exercises for Section 10.2 485

### 10.3 Binary Tree Nodes 485
- Pitfall: Not Connecting All the Links 488
- Programming Example: Animal Guessing 489
- Animal Guessing Program—Design and Implementation 491
- Animal Guessing Program—Improvements 496
- Self-Test Exercises for Section 10.3 500

### 10.4 Tree Traversals 500
- Traversals of Binary Trees 500
- Printing the Data from a Tree's Node 505
- The Problem with Our Traversals 506
- A Parameter Can Be a Function 507
- A Template Version of the Apply Function 509
- More Generality for the Apply Template Function 510
- Template Functions for Tree Traversals 511
- Self-Test Exercises for Section 10.4 512

### 10.5 Binary Search Trees 518
- The Binary Search Tree Storage Rules 518
- Our Sixth Bag—Class Definition 522
- Our Sixth Bag—Implementation of Some Simple Functions 522
- Counting the Occurrences of an Item in a Binary Search Tree 523
- Inserting a New Item into a Binary Search Tree 524
- Removing an Item from a Binary Search Tree 525
- The Update Operation for Binary Search Trees 529
- Time Analysis and an Iterator 531
- Self-Test Exercises for Section 10.5 531

- Chapter Summary 531
- Solutions to Self-Test Exercises 532
- Programming Projects 534

## CHAPTER 11 BALANCED TREES

### 11.1 Heaps 540
- The Heap Storage Rules 540
- The Priority Queue ADT with Heaps 541
- Adding an Entry to a Heap 542
- Removing an Entry from a Heap 543

### 11.2 The STL Priority Queue and Heap Algorithms 546
- Self-Test Exercises for Sections 11.1 and 11.2 547

### 11.3 B-Trees 547
- The Problem of Unbalanced Trees 547
- The B-Tree Rules 548
- An Example B-Tree 549
- The Set ADT with B-Trees 550
- Searching for an Item in a B-Tree 555
- Inserting an Item into a B-Tree 557
- The Loose Member Function 557
- A Private Member Function to Fix an Excess in a Child 560
- Back to the Insert Member Function 561
- Employing Top-Down Design 563
- Removing an Item from a B-Tree 563
- The Loose Erase from a B-Tree 564
- A Private Member Function to Fix a Shortage in a Child 566
- Removing the Biggest Item from a B-Tree 569
- Programming Tip: Write and Test Small Pieces 569
- Programming Tip: Consider Using the STL Vector 570
- External B-Trees 570
- Self-Test Exercises for Section 11.3 571

### 11.4 Trees, Logs, and Time Analysis 572
- Time Analysis for Binary Search Trees 573
- Time Analysis for Heaps 573
- Logarithms 575
- Logarithmic Algorithms 576
- Self-Test Exercises for Section 11.4 577

### 11.5 The STL Map and Multimap Classes 577
- Map and Multimap Implementations 578

- Chapter Summary 579
- Solutions to Self-Test Exercises 579
- Programming Projects 582

