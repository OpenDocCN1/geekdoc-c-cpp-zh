# # Chapter 8

# # General

# ### Question 1    Bit-fields and Concurrency

Which of the following data members are safe for concurrent updates ?

Program 8.1: Bit-fields and Concurrency

```
```
1 struct A
2 {
3     char non_bitfield_a;
4
5     int bitfield_b : 3;
6     int bitfield_c : 10;
7     int : 0;
8
9     int bitfield_d : 8;
10
11    struct E
12    {
13        int bitfield_a1 : 8;
14    } non_bitfield_e;
15
16    int bitfield_f : 4;
17    int non_bitfield_g;
18    int bitfield_h : 11;
19 };
```
```

# ### Solution of Question 1

As far as concurrent update is concerned, it is related to *memory location*, i.e., two threads of execution can safely update and access separate memory locations.

So let us try understanding the memory location of the member data, starting with bit-fields.

Program 8.2: Bit-fields and Concurrency

```
```
1 struct A
2 {
```
```