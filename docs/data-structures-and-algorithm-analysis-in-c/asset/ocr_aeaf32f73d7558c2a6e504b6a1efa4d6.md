```
1   int f ( )
2   {
3       IntCell a { 2 };
4       IntCell b = a;
5       IntCell c;
6
7       c = b;
8
9       a.write( 4 );
10      cout << a.read( ) << endl << b.read( ) << endl << c.read( ) << endl;
11
12      return 0;
13  }
```

# Figure 1.17 Simple function that exposes problems in Figure 1.16

The copy assignment operator at lines 16–21 uses a standard idiom of checking for aliasing at line 18 (i.e., a self-assignment, in which the client is making a call obj=obj) and then copying each data field in turn as needed. On completion, it returns a reference to itself using *this. In C++11, copy assignment is often written using a copy-and-swap idiom, leading to an alternate implementation:

```
16   IntCell & operator= ( const IntCell & rhs )    // Copy assignment
17   {
18       IntCell copy = rhs;
19       std::swap( *this, copy );
20       return *this;
21   }
```

Line 18 places a copy of rhs into copy using the copy constructor. Then this copy is swapped into *this, placing the old contents into copy. On return, a destructor is invoked for copy, cleaning up the old memory. For IntCell this is a bit inefficient, but for other types, especially those with many complex interacting data members, it can be a reasonably good default. Notice that if swap were implemented using the basic copy algorithm in Figure 1.14, the copy-and-swap idiom would not work, because there would be mutual non-terminating recursion. In C++11 we have a basic expectation that swapping is implemented either with three moves or by swapping member by member.

The move constructor at lines 13 and 14 moves the data representation from rhs into *this; then it sets rhs’s primitive data (including pointers) to a valid but easily destroyed state. Note that if there is non-primitive data, then that data must be moved in the initialization list. For example, if there were also vector<string> items, then the constructor would be:

```
IntCell( IntCell && rhs ) : storedValue( rhs.storedValue ),    // Move constructor
    items( std::move( rhs.items ) )
{ rhs.storedValue = nullptr; }
```