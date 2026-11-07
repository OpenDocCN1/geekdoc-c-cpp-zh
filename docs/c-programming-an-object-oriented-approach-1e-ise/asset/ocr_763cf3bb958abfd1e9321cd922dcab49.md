# **Program 9.7** Finding the larger between two objects (Continued)

```
```cpp
10
11 int main ( )
12 {
13    // Creating the first pair of fractions
14    Fraction fract1 (3, 13);
15    Fraction fract2 (5, 17);
16    cout << "Larger of the first pair of fraction: ";
17    larger (&fract1, &fract2) -> print ();
18    // Creating the second pair of fractions
19    Fraction fract3 (4, 9);
20    Fraction fract4 (1, 6);
21    cout << "Larger of the second pair of fractions: ";
22    larger (&fract3, &fract4) -> print ();
23    return 0;
24 }
25 /************************************************************
26  * The function gets two fractions by pointer, compares them  *
27  * and returns the larger of the two.                         *
28  ************************************************************/
29 Fraction* larger (Fraction* fract1, Fraction* fract2)
30 {
31    if (fract1 -> getNumer() * fract2 -> getDenom() >
32        fract2 -> getNumer() * fract1 -> getDenom())
33    {
34        return fract1;
35    }
36    return fract2;
37 }
```
```

```
```
Run:
Larger of first pair of fractions: 5/17
Larger of second pair of fractions: 4/9
```
```

# ## 9.3 ARRAYS AND POINTERS

In C++, arrays and pointers are intertwined with each other. In this section we learn how one-dimensional and two-dimensional arrays can be represented by pointers.

# ### 9.3.1 One-Dimensional Arrays and Pointers

When we declare an array named *arr* of type t and of capacity N, the system creates N memory locations of type t. The system then creates a constant pointer of type t that is pointed to the first element, as shown in Figure 9.15.

That the pointer is constant means its contents (address) cannot be changed. It is always pointing to the first element. Since the address of the first element is fixed, we know