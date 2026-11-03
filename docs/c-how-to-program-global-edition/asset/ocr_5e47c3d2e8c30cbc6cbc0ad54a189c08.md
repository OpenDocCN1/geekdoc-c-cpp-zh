```
```text
x: (0, 0)
y: (4.3, 8.2)
z: (3.3, 1.1)

x = y + z:
(7.6, 9.3) = (4.3, 8.2) + (3.3, 1.1)

x = y - z:
(1, 7.1) = (4.3, 8.2) - (3.3, 1.1)
```
```

**Fig. 18.16** | Complex class test program. (Part 2 of 2.)

**18.9 (HugeInt Class)** A machine with 32-bit integers can represent integers in the range of approximately –2 billion to +2 billion. This fixed-size restriction is rarely troublesome, but there are applications in which we would like to be able to use a much wider range of integers. This is what C++ was built to do, namely, create powerful new data types. Consider class HugeInt of Figs. 18.17–18.19. Study the class carefully, then answer the following:

+   a) Describe precisely how it operates.
+   b) What restrictions does the class have?
+   c) Overload the * multiplication operator.
+   d) Overload the / division operator.
+   e) Overload all the relational and equality operators.

> > [Note: We do not show an assignment operator or copy constructor for class HugeInt, because the assignment operator and copy constructor provided by the compiler are capable of copying the entire array data member properly.]

```
```cpp
1  // Fig. 18.17: HugeInt.h
2  // HugeInt class definition.
3  #ifndef HUGEINT_H
4  #define HUGEINT_H
5
6  #include <array>
7  #include <iostream>
8  #include <string>
9
10 class HugeInt
11 {
12    friend std::ostream &operator<<( std::ostream &, const HugeInt & );
13 public:
14    static const int digits = 30; // maximum digits in a HugeInt
15
16    HugeInt( long = 0 ); // conversion/default constructor
17    HugeInt( const std::string & ); // conversion constructor
18
19    // addition operator; HugeInt + HugeInt
20    HugeInt operator+( const HugeInt & ) const;
21
22    // addition operator; HugeInt + int
23    HugeInt operator+( int ) const;
24
25    // addition operator;
26    // HugeInt + string that represents large integer value
27    HugeInt operator+( const std::string & ) const;
```
```

**Fig. 18.17** | HugeInt class definition. (Part 1 of 2.)