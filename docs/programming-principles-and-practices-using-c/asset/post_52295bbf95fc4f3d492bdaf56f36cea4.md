
## Part II Input and Output 343

### Chapter 10 Input and Output Streams 345
- 10.1 Input and output 346
- 10.2 The I/O stream model 347
- 10.3 Files 349
- 10.4 Opening a file 350
- 10.5 Reading and writing a file 352
- 10.6 I/O error handling 354
- 10.7 Reading a single value 358
  - 10.7.1 Breaking the problem into manageable parts 359
  - 10.7.2 Separating dialog from function 362
- 10.8 User-defined output operators 363
- 10.9 User-defined input operators 365
- 10.10 A standard input loop 365
- 10.11 Reading a structured file 367
  - 10.11.1 In-memory representation 368
  - 10.11.2 Reading structured values 370
  - 10.11.3 Changing representations 374

### Chapter 11 Customizing Input and Output 379
- 11.1 Regularity and irregularity 380
- 11.2 Output formatting 380
  - 11.2.1 Integer output 381
  - 11.2.2 Integer input 383
  - 11.2.3 Floating-point output 384
  - 11.2.4 Precision 385
  - 11.2.5 Fields 387
- 11.3 File opening and positioning 388
  - 11.3.1 File open modes 388
  - 11.3.2 Binary files 390
  - 11.3.3 Positioning in files 393
- 11.4 String streams 394
- 11.5 Line-oriented input 395
- 11.6 Character classification 396
- 11.7 Using nonstandard separators 398
- 11.8 And there is so much more 406

### Chapter 12 A Display Model 411
- 12.1 Why graphics? 412
- 12.2 A display model 413
- 12.3 A first example 414
- 12.4 Using a GUI library 418
- 12.5 Coordinates 419
- 12.6 Shapes 420
- 12.7 Using Shape primitives 421
  - 12.7.1 Graphics headers and main 421
  - 12.7.2 An almost blank window 422
  - 12.7.3 Axis 424
  - 12.7.4 Graphing a function 426
  - 12.7.5 Polygons 427
  - 12.7.6 Rectangles 428
  - 12.7.7 Fill 431
  - 12.7.8 Text 431
  - 12.7.9 Images 433
  - 12.7.10 And much more 434
- 12.8 Getting this to run 435
  - 12.8.1 Source files 437

### Chapter 13 Graphics Classes 441
- 13.1 Overview of graphics classes 442
- 13.2 Point and Line 444
- 13.3 Lines 447
- 13.4 Color 450
- 13.5 Line_style 452
- 13.6 Open_polyline 455
- 13.7 Closed_polyline 456
- 13.8 Polygon 458
- 13.9 Rectangle 460
- 13.10 Managing unnamed objects 465
- 13.11 Text 467
- 13.12 Circle 470
- 13.13 Ellipse 472
- 13.14 Marked_polyline 474
- 13.15 Marks 476
- 13.16 Mark 478
- 13.17 Images 479

### Chapter 14 Graphics Class Design 487
- 14.1 Design principles 488
  - 14.1.1 Types 488
  - 14.1.2 Operations 490
  - 14.1.3 Naming 491
  - 14.1.4 Mutability 492
- 14.2 Shape 493
  - 14.2.1 An abstract class 495
  - 14.2.2 Access control 496
  - 14.2.3 Drawing shapes 500
  - 14.2.4 Copying and mutability 503
- 14.3 Base and derived classes 504
  - 14.3.1 Object layout 506
  - 14.3.2 Deriving classes and defining virtual functions 507
  - 14.3.3 Overriding 508
  - 14.3.4 Access 511
  - 14.3.5 Pure virtual functions 512
- 14.4 Benefits of object-oriented programming 513

### Chapter 15 Graphing Functions and Data 519
- 15.1 Introduction 520
- 15.2 Graphing simple functions 520
- 15.3 Function 524
  - 15.3.1 Default Arguments 525
  - 15.3.2 More examples 527
  - 15.3.3 Lambda expressions 528
- 15.4 Axis 529
- 15.5 Approximation 532
- 15.6 Graphing data 537
  - 15.6.1 Reading a file 539
  - 15.6.2 General layout 541
  - 15.6.3 Scaling data 542
  - 15.6.4 Building the graph 543

### Chapter 16 Graphical User Interfaces 551
- 16.1 User interface alternatives 552
- 16.2 The “Next” button 553
- 16.3 A simple window 554
  - 16.3.1 A callback function 556
  - 16.3.2 A wait loop 559
  - 16.3.3 A lambda expression as a callback 560
- 16.4 Button and other Widgets 561
  - 16.4.1 Widgets 561
  - 16.4.2 Buttons 563
  - 16.4.3 In_box and Out_box 563
  - 16.4.4 Menus 564
- 16.5 An example 565
- 16.6 Control inversion 569
- 16.7 Adding a menu 570
- 16.8 Debugging GUI code 575

## Part III Data and Algorithms 581

### Chapter 17 Vector and Free Store 583
- 17.1 Introduction 584
- 17.2 vector basics 586
- 17.3 Memory, addresses, and pointers 588
  - 17.3.1 The sizeof operator 590
- 17.4 Free store and pointers 591
  - 17.4.1 Free-store allocation 593
  - 17.4.2 Access through pointers 594
  - 17.4.3 Ranges 595
  - 17.4.4 Initialization 596
  - 17.4.5 The null pointer 598
  - 17.4.6 Free-store deallocation 598
- 17.5 Destructors 601
  - 17.5.1 Generated destructors 603
  - 17.5.2 Destructors and free store 604
- 17.6 Access to elements 605
- 17.7 Pointers to class objects 606
- 17.8 Messing with types: void* and casts 608
- 17.9 Pointers and references 610
  - 17.9.1 Pointer and reference parameters 611
  - 17.9.2 Pointers, references, and inheritance 612
  - 17.9.3 An example: lists 613
  - 17.9.4 List operations 615
  - 17.9.5 List use 616
- 17.10 The this pointer 618
  - 17.10.1 More link use 620

### Chapter 18 Vectors and Arrays 627
- 18.1 Introduction 628
- 18.2 Initialization 629
- 18.3 Copying 631
  - 18.3.1 Copy constructors 633
  - 18.3.2 Copy assignments 634
  - 18.3.3 Copy terminology 636
  - 18.3.4 Moving 637
- 18.4 Essential operations 640
  - 18.4.1 Explicit constructors 642
  - 18.4.2 Debugging constructors and destructors 643
- 18.5 Access to vector elements 646
  - 18.5.1 Overloading on const 647
- 18.6 Arrays 648
  - 18.6.1 Pointers to array elements 650
  - 18.6.2 Pointers and arrays 652
  - 18.6.3 Array initialization 654
  - 18.6.4 Pointer problems 656
- 18.7 Examples: palindrome 659
  - 18.7.1 Palindromes using string 659
  - 18.7.2 Palindromes using arrays 660
  - 18.7.3 Palindromes using pointers 661

### Chapter 19 Vector, Templates, and Exceptions 667
- 19.1 The problems 668
- 19.2 Changing size 671
  - 19.2.1 Representation 671
  - 19.2.2 reserve and capacity 673
  - 19.2.3 resize 674
  - 19.2.4 push_back 674
  - 19.2.5 Assignment 675
  - 19.2.6 Our vector so far 677
- 19.3 Templates 678
  - 19.3.1 Types as template parameters 679
  - 19.3.2 Generic programming 681
  - 19.3.3 Concepts 683
  - 19.3.4 Containers and inheritance 686
  - 19.3.5 Integers as template parameters 687
  - 19.3.6 Template argument deduction 689
  - 19.3.7 Generalizing vector 690
- 19.4 Range checking and exceptions 693
  - 19.4.1 An aside: design considerations 694
  - 19.4.2 A confession: macros 696
- 19.5 Resources and exceptions 697
  - 19.5.1 Potential resource management problems 698
  - 19.5.2 Resource acquisition is initialization 700
  - 19.5.3 Guarantees 701
  - 19.5.4 unique_ptr 703
  - 19.5.5 Return by moving 704
  - 19.5.6 RAII for vector 705

### Chapter 20 Containers and Iterators 711
- 20.1 Storing and processing data 712
  - 20.1.1 Working with data 713
  - 20.1.2 Generalizing code 714
- 20.2 STL ideals 717
- 20.3 Sequences and iterators 720
  - 20.3.1 Back to the example 723
- 20.4 Linked lists 724
  - 20.4.1 List operations 726
  - 20.4.2 Iteration 727
- 20.5 Generalizing vector yet again 729
  - 20.5.1 Container traversal 732
  - 20.5.2 auto 732
- 20.6 An example: a simple text editor 734
  - 20.6.1 Lines 736
  - 20.6.2 Iteration 737
- 20.7 vector, list, and string 741
  - 20.7.1 insert and erase 742
- 20.8 Adapting our vector to the STL 745
- 20.9 Adapting built-in arrays to the STL 747
- 20.10 Container overview 749
  - 20.10.1 Iterator categories 751

### Chapter 21 Algorithms and Maps 757
- 21.1 Standard library algorithms 758
- 21.2 The simplest algorithm: find() 759
  - 21.2.1 Some generic uses 761
- 21.3 The general search: find_if() 763
- 21.4 Function objects 765
  - 21.4.1 An abstract view of function objects 766
  - 21.4.2 Predicates on class members 767
  - 21.4.3 Lambda expressions 769
- 21.5 Numerical algorithms 770
  - 21.5.1 Accumulate 770
  - 21.5.2 Generalizing accumulate() 772
  - 21.5.3 Inner product 774
  - 21.5.4 Generalizing inner_product() 775
- 21.6 Associative containers 776
  - 21.6.1 map 776
  - 21.6.2 map overview 779
  - 21.6.3 Another map example 782
  - 21.6.4 unordered_map 785
  - 21.6.5 set 787
- 21.7 Copying 789
  - 21.7.1 Copy 789
  - 21.7.2 SStream iterators 790
  - 21.7.3 Using a set to keep order 793
  - 21.7.4 copy_if 794
- 21.8 Sorting and searching 794
- 21.9 Container algorithms 797

## Part IV Broadening the View 803

### Chapter 22 Ideals and History 805
- 22.1 History, ideals, and professionalism 806
  - 22.1.1 Programming language aims and philosophies 807
  - 22.1.2 Programming ideals 808
  - 22.1.3 Styles/paradigms 815
- 22.2 Programming language history overview 818
  - 22.2.1 The earliest languages 819
  - 22.2.2 The roots of modern languages 821
  - 22.2.3 The Algol family 826
  - 22.2.4 Simula 833
  - 22.2.5 C 836
  - 22.2.6 C++ 839
  - 22.2.7 Today 842
  - 22.2.8 Information sources 844

### Chapter 23 Text Manipulation 849
- 23.1 Text 850
- 23.2 Strings 850
- 23.3 I/O streams 855
- 23.4 Maps 855
  - 23.4.1 Implementation details 861
- 23.5 A problem 864
- 23.6 The idea of regular expressions 866
  - 23.6.1 Raw string literals 868
- 23.7 Searching with regular expressions 869
- 23.8 Regular expression syntax 872
  - 23.8.1 Characters and special characters 872
  - 23.8.2 Character classes 873
  - 23.8.3 Repeats 874
  - 23.8.4 Grouping 876
  - 23.8.5 Alternation 876
  - 23.8.6 Character sets and ranges 877
  - 23.8.7 Regular expression errors 878
