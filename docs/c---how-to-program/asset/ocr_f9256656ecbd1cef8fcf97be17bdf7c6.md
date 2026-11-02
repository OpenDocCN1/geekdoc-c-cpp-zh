> > **Error-Prevention Tip 17.4**
> >
> > *To make your code clearer and more maintainable, and to avoid errors, never hide data members with local variable names.*

# ### Type of the *this* Pointer

The type of the *this* pointer depends on the type of the object and whether the member function in which *this* is used is declared const. For example, in a non-const member function of class `Employee`, the *this* pointer has the type `Employee *`. In a const member function, the *this* pointer has the type `const Employee *`.

# ### Implicitly and Explicitly Using the *this* Pointer to Access an Object's Data Members

Figure 17.23 demonstrates the implicit and explicit use of the *this* pointer to enable a member function of class `Test` to print the private data `x` of a `Test` object. In the next example and in Chapter 18, we show some substantial and subtle examples of using *this*.

```
```cpp
1  // Fig. 17.23: fig17_23.cpp
2  // Using the this pointer to refer to object members.
3  #include <iostream>
4  using namespace std;
5
6  class Test
7  {
8  public:
9      explicit Test( int = 0 ); // default constructor
10     void print() const;
11 private:
12     int x;
13 }; // end class Test
14
15 // constructor
16 Test::Test( int value )
17     : x( value ) // initialize x to value
18 {
19     // empty body
20 } // end constructor Test
21
22 // print x using implicit and explicit this pointers;
23 // the parentheses around *this are required
24 void Test::print() const
25 {
26     // implicitly use the this pointer to access the member x
27     cout << "    x = " << x;
28
29     // explicitly use the this pointer and the arrow operator
30     // to access the member x
31     cout << "\n  this->x = " << this->x;
32
```
```

**Fig. 17.23** | using the *this* pointer to refer to object members. (Part 1 of 2.)