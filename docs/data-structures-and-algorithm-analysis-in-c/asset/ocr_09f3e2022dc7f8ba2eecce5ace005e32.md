```
1 class IntCell
2 {
3 public:
4 explicit IntCell( int initialValue = 0 )
5 { storedValue = new int{ initialValue }; }
6
7 ~IntCell( )
8 { delete storedValue; } // Destructor
9
10 IntCell( const IntCell & rhs ) // Copy constructor
11 { storedValue = new int{ *rhs.storedValue }; }
12
13 IntCell( IntCell && rhs ) : storedValue{ rhs.storedValue } // Move constructor
14 { rhs.storedValue = nullptr; }
15
16 IntCell & operator= ( const IntCell & rhs ) // Copy assignment
17 {
18 if( this != &rhs )
19 *storedValue = *rhs.storedValue;
20
21 return *this;
22 }
23
24 IntCell & operator= ( IntCell && rhs ) // Move assignment
25 {
26 std::swap( storedValue, rhs.storedValue );
27 return *this;
28 }
29
30 int read( ) const
31 { return *storedValue; }
32
33 void write( int x )
34 { *storedValue = x; }
35
36 private:
37 int *storedValue;
38 };
```

# Figure 1.18 Data member is a pointer; big-five is written

Finally, the move assignment operator at lines 23–27 is implemented as a member-by-member swap. Note that sometimes it is implemented as a single swap of objects in the same manner as the copy assignment operator, but that only works if swap itself is implemented as a member-by-member swap. If swap is implemented as three moves, then we would have mutual nonterminating recursion.

# 1.5.7 C-style Arrays and Strings

The C++ language provides a built-in C-style array type. To declare an array, arr1, of 10 integers, one writes:

```
int arr1[ 10 ];
```