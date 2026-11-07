
## 13 Stream Input/Output: A Deeper Look　　562
- 13.1 Introduction　　563
- 13.2 Streams　　564
    - 13.2.1 Classic Streams vs. Standard Streams　　564
    - 13.2.2 iostream Library Headers　　565
    - 13.2.3 Stream Input/Output Classes and Objects　　565
- 13.3 Stream Output　　567
    - 13.3.1 Output of char * Variables　　568
    - 13.3.2 Character Output Using Member Function put　　568
- 13.4 Stream Input　　569
    - 13.4.1 get and getline Member Functions　　569
    - 13.4.2 iostream Member Functions peek, putback and ignore　　572
    - 13.4.3 Type-Safe I/O　　572
- 13.5 Unformatted I/O Using read, write and gcount　　572
- 13.6 Introduction to Stream Manipulators　　573
    - 13.6.1 Integral Stream Base: dec, oct, hex and setbase　　574
    - 13.6.2 Floating-Point Precision (precision, setprecision)　　574
    - 13.6.3 Field Width (width, setw)　　576
    - 13.6.4 User-Defined Output Stream Manipulators　　577
- 13.7 Stream Format States and Stream Manipulators　　578
    - 13.7.1 Trailing Zeros and Decimal Points (showpoint)　　579
    - 13.7.2 Justification (left, right and internal)　　580
    - 13.7.3 Padding (fill, setfill)　　582
    - 13.7.4 Integral Stream Base (dec, oct, hex, showbase)　　583
    - 13.7.5 Floating-Point Numbers; Scientific and Fixed Notation (scientific, fixed)　　584
    - 13.7.6 Uppercase/Lowercase Control (uppercase)　　585
    - 13.7.7 Specifying Boolean Format (boolalpha)　　585
    - 13.7.8 Setting and Resetting the Format State via Member Function flags　　586
- 13.8 Stream Error States　　587
- 13.9 Tying an Output Stream to an Input Stream　　590
- 13.10 Wrap-Up　　590

## 14 File Processing　　599
- 14.1 Introduction　　600
- 14.2 Files and Streams　　600
- 14.3 Creating a Sequential File　　601
- 14.4 Reading Data from a Sequential File　　605
- 14.5 Updating Sequential Files　　611
- 14.6 Random-Access Files ........ 611
- 14.7 Creating a Random-Access File ........ 612
- 14.8 Writing Data Randomly to a Random-Access File ........ 617
- 14.9 Reading from a Random-Access File Sequentially ........ 619
- 14.10 Case Study: A Transaction-Processing Program ........ 621
- 14.11 Object Serialization ........ 628
- 14.12 Wrap-Up ........ 628

## 15 Standard Library Containers and Iterators ......... 638
- 15.1 Introduction ......... 639
- 15.2 Introduction to Containers ......... 640
- 15.3 Introduction to Iterators ......... 644
- 15.4 Introduction to Algorithms ......... 649
- 15.5 Sequence Containers ......... 649
    - 15.5.1 vector Sequence Container ......... 650
    - 15.5.2 list Sequence Container ......... 658
    - 15.5.3 deque Sequence Container ......... 662
- 15.6 Associative Containers ......... 664
    - 15.6.1 multiset Associative Container ......... 665
    - 15.6.2 set Associative Container ......... 668
    - 15.6.3 multimap Associative Container ......... 669
    - 15.6.4 map Associative Container ......... 671
- 15.7 Container Adapters ......... 673
    - 15.7.1 stack Adapter ......... 673
    - 15.7.2 queue Adapter ......... 675
    - 15.7.3 priority_queue Adapter ......... 676
- 15.8 Class bitset ......... 677
- 15.9 Wrap-Up ......... 679

## 16 Standard Library Algorithms ......... 690
- 16.1 Introduction ......... 691
- 16.2 Minimum Iterator Requirements ......... 691
- 16.3 Algorithms ......... 693
    - 16.3.1 fill, fill_n, generate and generate_n ......... 693
    - 16.3.2 equal, mismatch and lexicographical_compare ......... 695
    - 16.3.3 remove, remove_if, remove_copy and remove_copy_if ......... 697
    - 16.3.4 replace, replace_if, replace_copy and replace_copy_if ......... 700
    - 16.3.5 Mathematical Algorithms ......... 702
    - 16.3.6 Basic Searching and Sorting Algorithms ......... 706
    - 16.3.7 swap, iter_swap and swap_ranges ........ 710
    - 16.3.8 copy_backward, merge, unique and reverse ........ 711
    - 16.3.9 inplace_merge, unique_copy and reverse_copy ........ 714
    - 16.3.10 Set Operations ........ 716
    - 16.3.11 lower_bound, upper_bound and equal_range ........ 719
    - 16.3.12 Heapsort ........ 721
    - 16.3.13 min, minmax and minmax_element ........ 724
- 16.4 Function Objects ........ 726
- 16.5 Lambda Expressions ........ 729
- 16.6 Standard Library Algorithm Summary ........ 730
- 16.7 Wrap-Up ........ 732

## 17 Exception Handling: A Deeper Look ........ 740
- 17.1 Introduction ........ 741
- 17.2 Example: Handling an Attempt to Divide by Zero ........ 741
- 17.3 Rethrowing an Exception ........ 747
- 17.4 Stack Unwinding ........ 748
- 17.5 When to Use Exception Handling ........ 750
- 17.6 Constructors, Destructors and Exception Handling ........ 751
- 17.7 Exceptions and Inheritance ........ 752
- 17.8 Processing new Failures ........ 752
- 17.9 Class unique_ptr and Dynamic Memory Allocation ........ 755
- 17.10 Standard Library Exception Hierarchy ........ 758
- 17.11 Wrap-Up ........ 759

## 18 Introduction to Custom Templates ........ 765
- 18.1 Introduction ........ 766
- 18.2 Class Templates ........ 766
- 18.3 Function Template to Manipulate a Class-Template Specialization Object ........ 771
- 18.4 Nontype Parameters ........ 773
- 18.5 Default Arguments for Template Type Parameters ........ 773
- 18.6 Overloading Function Templates ........ 774
- 18.7 Wrap-Up ........ 774

## 19 Custom Templatized Data Structures ........ 777
- 19.1 Introduction ........ 778
- 19.2 Self-Referential Classes ........ 779
- 19.3 Linked Lists ........ 780
- 19.4 Stacks ........ 794
- 19.5 Queues ........ 799
- 19.6 Trees ......... 803
- 19.7 Wrap-Up ......... 811

## 20 Searching and Sorting ........ 822
- 20.1 Introduction ........ 823
- 20.2 Searching Algorithms ......... 824
    - 20.2.1 Linear Search ........ 824
    - 20.2.2 Binary Search ........ 827
- 20.3 Sorting Algorithms ........ 831
    - 20.3.1 Insertion Sort ........ 832
    - 20.3.2 Selection Sort ........ 834
    - 20.3.3 Merge Sort (A Recursive Implementation) ........ 837
- 20.4 Wrap-Up ......... 843

## 21 Class string and String Stream Processing: A Deeper Look ........ 849
- 21.1 Introduction ........ 850
- 21.2 string Assignment and Concatenation ........ 851
- 21.3 Comparing strings ........ 853
- 21.4 Substrings ......... 856
- 21.5 Swapping strings ......... 856
- 21.6 string Characteristics ......... 857
- 21.7 Finding Substrings and Characters in a string ........ 859
- 21.8 Replacing Characters in a string ......... 861
- 21.9 Inserting Characters into a string ......... 863
- 21.10 Conversion to Pointer-Based char * Strings ........ 864
- 21.11 Iterators ......... 865
- 21.12 String Stream Processing ......... 867
- 21.13 C++11 Numeric Conversion Functions ......... 870
- 21.14 Wrap-Up ......... 871

## 22 Bits, Characters, C Strings and structs ........ 879
- 22.1 Introduction ........ 880
- 22.2 Structure Definitions ......... 880
- 22.3 typedef ......... 882
- 22.4 Example: Card Shuffling and Dealing Simulation ......... 882
