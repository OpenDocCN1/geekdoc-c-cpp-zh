a stack of integers that uses a vector of integers as its underlying data structure. Line 26 specifies a stack of integers that uses a list of integers as its underlying data structure.

Function pushElements (lines 49–56) pushes the elements onto each stack. Line 53 uses function push (available in each adapter class) to place an integer on top of the stack. Line 54 uses stack function top to retrieve the top element of the stack for output. Function top does not remove the top element.

Function popElements (lines 59–66) pops the elements off each stack. Line 63 uses stack function top to retrieve the top element of the stack for output. Line 64 uses function pop (available in each adapter class) to remove the top element of the stack. Function pop does not return a value.

```
1  // Fig. 20.23: fig20_23.cpp
2  // Standard Library adapter stack test program.
3  #include <iostream>
4  using std::cout;
5  using std::endl;
6  
7  #include <stack> // stack adapter definition
8  #include <vector> // vector class-template definition
9  #include <list> // list class-template definition
10 
11  // pushElements function-template prototype
12  template< typename T > void pushElements( T &stackRef );
13 
14  // popElements function-template prototype
15  template< typename T > void popElements( T &stackRef );
16 
17  int main()
18  {
19      // stack with default underlying deque
20      std::stack< int > intDequeStack;
21  
22      // stack with underlying vector
23      std::stack< int, std::vector< int > > intVectorStack;
24  
25      // stack with underlying list
26      std::stack< int, std::list< int > > intListStack;
27  
28      // push the values 0-9 onto each stack
29      cout << "Pushing onto intDequeStack: ";
30      pushElements( intDequeStack );
31      cout << "\nPushing onto intVectorStack: ";
32      pushElements( intVectorStack );
33      cout << "\nPushing onto intListStack: ";
34      pushElements( intListStack );
35      cout << endl << endl;
36  
37      // display and remove elements from each stack
38      cout << "Popping from intDequeStack: ";
39      popElements( intDequeStack );
```