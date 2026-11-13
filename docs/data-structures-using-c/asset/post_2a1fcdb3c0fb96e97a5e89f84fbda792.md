
const Complex &
} );

Complex operator + (const Complex &op1, const Complex &op2)
{
    double Real = op1.Real + op2.Real;
    double Imag = op1.Imag + op2.Imag;
    return(Complex(Real, Imag));
}

The only change in using friend functions for operator overloading is that they do not have 'this' pointer. They cannot access the class members directly. They access class members using objects that are passed as arguments to them. They can be declared in the public or private sections of a class without any consequence.

## A.14 GENERIC PROGRAMMING: TEMPLATES

A stack of integers is often defined as follows:

```
class Intstack
{
    int Top;
    int Data[20];
    public:
    Intstack()
    {
        Top = -1;
    }
    void Push(int);
    int TopElement();
    void Pop();
} S1, S2;
```

This class can be used as a blue print for creating objects, which are stacks of integers such as S1 and S2. The class has private data members, such as Top and Data, and member functions to operate on. When we need to create a stack of real numbers, we need to define a separate class as follows:

```
class Floatstack
{
    int Top;
    float Data[20];
    public:
    Floatstack()
    {
        Top = -1;
    }
    void Push(float);
    float TopElement();
    void Pop();
} S3, S4;
```

Here, S3 and S4 are stacks for storing real numbers. To avoid defining two similar stacks, which vary only in the type of data being processed, templates are used. When we need to perform the same operation on different data types, we can use function templates. Template is the most powerful feature of C++ that enables software reuse. Templates help in defining generic functions and classes. They allow the user to specify the type of data as a parameter.

Using templates, the two classes Intstack and Floatstack can be defined as a single class as follows:

```
template <class T>
class stack
{
    int Top;
    T Data[20];
    public:
    stack()
    {
        Top = -1;
    }
    void Push(T);
    T TopElement();
    void Pop();
};
```

```
stack <int> S1, S2; // integer stacks
stack <float> S3, S4; // float stacks
```

## ACKNOWLEDGEMENTS

I would like to thank many people who encouraged and helped me in various ways throughout this project, namely, my family, my didi Megha and Arvindji jai, my colleagues, friends, and students.

First and foremost I would like to acknowledge Dr Gajanan Kharate, Dr Shrish Sane, Vaishali Pawar, Vaishali Tidke, Seema Gondhalekar, Swati Bhavsar, Alpana Borse, Snehal Umare, and all my colleagues. Special thanks to Mr Mahesh Sanghvi for his untiring efforts in making this project successful. This book would not have been what it is, without him.

I received constant support and motivation from honourable Balasahebwagh, Narendrabhau, Kishorbhau, Laxmanbhau, and Kunal Darabe. I thank them for all the inspiration.

My husband, Hemant, encouraged me even before I started writing this book. His contagious enthusiasm and generous spirit and also the ever-smiling faces of my children Abolee and Saurabh made working on this project a pleasant experience. Finally, I would like to thank my parents, sisters, brother, and all other family members for making the experience of writing this book memorable.

Last but not the least, my acknowledgements would remain incomplete if I do not thank the editorial team of Oxford University Press, India, who supported me throughout the development of this manuscript.

Dr Varsha H. Patil

## INDEX

| Index Terms | Links |
| --- | --- |
| A | |
| AA tree | 634 635 636 |
| Abstract | 6 7 8 21<br>188 207 296 678<br>686 |
| Abstract data type (ADT) | 1 3 7 21<br>30 36 89 95<br>99 169 297 373<br>552 560 612 677-679<br>683 690 |
| Adjacency list | 375 378 379-381 383<br>384-388 391 392 415 |
| Adjacency matrix | 375 376-378 380 384<br>385 387 391 412<br>415 |
| Adjacency multilist | 375 383 384 415 |
| ADT | 1 3 7 21<br>30 36 89 95<br>99 169 297 373<br>552 560 612 677<br>679 683 690 |
| ADT array | 37 |
| Algorithm | 2 3 4 11-32<br>64 70 93 256<br>289 296 306 312<br>322 361 371 398 |
| Algorithm (Cont.) | 408 421 573 626 634 642 655 677 704 |
| Algorithmics | 13 |
| Algorithmic strategies | 714 715 716 |
| Analysis of algorithms | 13 20 22 30 756 |
| Array | 5 9 10 33-37 46 203 243-245 249 298 299 399 421 448 467 481 551 639 688 698 704 |
| base | 35 38 39 49 53 142 161 297 |
| data type of an array | 35 |
| direct access | 9 11 30 34-36 38 89 91 95 197 199 251 304 325 385 421 638 640 641 655 663 683 |
| index | 34-36 59 63 89 102 163 164 170 180 300 422 436 528 589 |
| range of index | 36 |
| size of array | 35 41 |
| value | 34 35 37 38 69 84 89 |
| Asymptotic notations | 715 756 |
| big O | 25 26 715 758 |
| omega | 715 716 |
| theta | 715 |
| Atomic data | 4 |
| AVL tree | 280 500 509 510<br>514 515 517-520 522<br>523 593 631 635 |
| B | |
| Biconnected components | 407 416 |
| merge-find set | 408 |
| union-find data structure | 408 |
| | 16 20 154 159 |
| Binary search | 165 280 325 326<br>361 376 424-428 475<br>718 |
| Binary search tree (BST) | 280 325 326 333<br>340 367 479 481<br>552 556 593 598 |
| Binary tree | 280 290 292-308 539<br>556 567 593 723 |
| Binary tree traversal | 304 |
| inorder | 280 307 312 315<br>318 332 344 481 |
| postorder | 308 313 315 318<br>352 367 |
| preorder | 306 307 315 318<br>391 |
| Binomial heap | 579-583 |
| Binomial tree | 579-582 |
| Boyer-Moore algorithm | 743 747 748 |
| Breadth-first search (BFS) | 385 386 416 |
| Breadth-first traversal | 309 317 319 385<br>585 |
| Brute-force approach | 743 746 747 |
| B+ tree | 593 624-628 637 |
| B-tree | 589 594 597 598<br>600 624 631 |
| Bubble sort | 433 437-443 447 472<br>475 |
| Bucket sort | 438 440 461 463<br>464 |
| C | |
| Cellular partition | 672 |
| Circular linked list | 216 226 227 237-241<br>276 |
| non-circular or grounded list | 227 |
| two-way list | 228 |
| Circular queue | 168 176 177 180<br>186 192 256 |
| Class | 5 292 361 483<br>643 677 682 691<br>704 706 711 |
| Collision resolution strategies | 527 535 |
| chaining | 535 545 546 548<br>550 657 |
| double hashing | 535 541 542 544 |
| linear probing | 535-540 542-545 548-550 |
| linear probing without replacement | 538 |
| linear probing with replacement | 537 |
| Collision resolution strategies (Cont.) | |
| open addressing | 535 536 542 544<br>548 549 |
| open addressing using double hash function | 545 |
| open addressing using linear probing | 543 544 |
| open addressing using quadratic probing | 543 544 |
| quadratic probing | 535 539-545 |
| rehashing | 531 536 544-549 550 |
| Column-major representation | 48 50-52 91 |
| Compiler | 3 24 30 36<br>93 110 112 113<br>162 199 206 308<br>436 479 480 523<br>527 684 691 710 |
| Complexity of algorithms | 13 22 23 |
| Composite data | 4 5 21 34 |
| Computer | 1-9 11 13 23<br>26 38 58 91<br>96 110 141 183<br>224 262 367 372<br>466 481 633 |
| Computer languages | 2 |
| assembly | 2 31 |
| high-level | 2 3 716 |
| machine | 2 3 31 110 |
| Connected component | 284 397 398 403<br>407 419 |
| Containers | 691-693 702 703 710<br>711 |
| associative | 692 703 711 |
| sequence | 692 712 |
| Contiguous stack | 100 107 144 254 |
| Coral ring | 671 |
| Cylinder-surface indexing | 591 592 |
| D | |
| Data | 1-4 124 132 300<br>391 396 408 414<br>420 546 548 552-553<br>556 564 568 580<br>590 754 |
| atomic | 4 |
| composite | 4 5 21 34 |
| Data structure | 1-21 77 166 174<br>192 309 311 319<br>323 399 408 428<br>527 551 624 678<br>691 753 |
| Data type | 1 3 4 21<br>30 35 89 169<br>207 224 253 296<br>373 552 560 612<br>638 677 690 698<br>711 |
| built-in | 4 5 9 11 |
| user-defined | 46 |
| Decision tree | 280 355 359 367<br>370 |
| Delete | 41 44 90 92<br>93 98 103 206<br>277 458 469 514<br>551 560 566 572<br>576 584 696 699 |
