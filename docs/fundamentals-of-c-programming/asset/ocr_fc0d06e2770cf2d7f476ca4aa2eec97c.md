```
void f() {
    IntList3 seq1, seq2; // Create two empty integer linked lists

    seq1.insert(10); // Build the list [10]-->[-2]-->[8]
    seq1.insert(-2);
    seq1.insert(8);
    seq1.print();

    seq2.insert(5); // Build the list [5]-->[4]
    seq2.insert(4);
    seq2.print();

    std::cout << "\n--------------\n";

    seq1 = seq2; // What does this do?
    seq1.print();
}

int main() {
    f();
    std::cout << "All done\n";
}
```

Listing 18.13 (listassign.cpp) builds two separate linked lists and then assigns one list to the other. On one system the program prints

```
Creating node 10 (14457304)
Creating node -2 (14457592)
Creating node 8 (14456152)
10 -> -2 -> 8
Creating node 5 (14456200)
Creating node 4 (14456248)
5 4
---------------
5 4
Destroying node 4 (14456248)
Destroying node 5 (14456200)
Destroying node 4 (14456248)
Destroying node 5 (14456200)
All done
```

During this particular run the program ran to completion; however, sometimes the program will crash before printing All done. On some systems the program crashes before printing the last three lines of output.

During this run of Listing 18.13 (listassign.cpp) the output shows that the program never destroys the nodes containing 10, -2, and 8. Further, the program destroys the nodes containing 4 and 5 twice! We can see the program deletes the same memory twice by comparing the memory addresses in parentheses. This undefined behavior of double deletion is what causes the program to crash at times.

The problem is in this statement:

```
seq1 = seq2;
```

What exactly does this statement do?