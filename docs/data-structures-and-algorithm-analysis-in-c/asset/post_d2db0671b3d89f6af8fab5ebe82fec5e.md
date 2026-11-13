
vector<int> daysInMonth( 12 ); // No { } before C++11
daysInMonth[ 0 ] = 31; daysInMonth[ 1 ] = 28; daysInMonth[ 2 ] = 31;
daysInMonth[ 3 ] = 30; daysInMonth[ 4 ] = 31; daysInMonth[ 5 ] = 30;
daysInMonth[ 6 ] = 31; daysInMonth[ 7 ] = 31; daysInMonth[ 8 ] = 30;
daysInMonth[ 9 ] = 31; daysInMonth[ 10 ] = 30; daysInMonth[ 11 ] = 31;

Certainly this leaves something to be desired. C++11 fixes this problem and allows:

```
vector<int> daysInMonth = { 31, 28, 31, 30, 31, 30, 31, 30, 31, 30, 31 };
```

Requiring the = in the initialization violates the spirit of uniform initialization, since now we would have to remember when it would be appropriate to use =. Consequently, C++11 also allows (and some prefer):

```
vector<int> daysInMonth { 31, 28, 31, 30, 31, 30, 31, 30, 31, 30, 31 };
```

With syntax, however, comes ambiguity, as one sees with the declaration

```
vector<int> daysInMonth ( 12 );
```

Is this a vector of size 12, or is it a vector of size 1 with a single element 12 in position 0? C++11 gives precedence to the initializer list, so in fact this is a vector of size 1 with a single element 12 in position 0, and if the intention is to initialize a vector of size 12, the old C++ syntax using parentheses must be used:

```
vector<int> daysInMonth( 12 ); // Must use ( ) to call constructor that takes size
```

string is also easy to use and has all the relational and equality operators to compare the strings of two strings. Thus str1<=str2 is true if the value of the strings are the same. It also has a length method that returns the string length.

As Figure 1.10 shows, the basic operation on arrays is indexing with []. Thus, the sum of the squares can be computed as:

```
int sum = 0;
for ( int i = 0; i < squares.size( ); ++i )
 sum += squares[ i ];
```

The pattern of accessing every element sequentially in a collection such as an array or a vector is fundamental, and using array indexing for this purpose does not clearly express the idiom. C++11 adds a range for syntax for this purpose. The above fragment can be written instead as:

```
int sum = 0;
for ( int x : squares )
 sum += x;
```

In many cases, the declaration of the type in the range for statement is unneeded; if squares is a vector<int>, it is obvious that x is intended to be an int. Thus C++11 also allows the use of the reserved word auto to signify that the compiler will automatically infer the appropriate type:

```
int sum = 0;
for ( auto x : squares )
 sum += x;
```

The range for loop is appropriate only if every item is being accessed sequentially and only if the index is not needed. Thus, in Figure 1.10 the two loops cannot be rewritten as range for loops, because the index i is also being used for other purposes. The range for loop as shown so far allows only the viewing of items; changing the items can be done using syntax described in Section 1.5.4.

## 1.5 C++ Details

Like any language, C++ has its share of details and language features. Some of these are discussed in this section.

### 1.5.1 Pointers

A pointer variable is a variable that stores the address where another object resides. It is the foundational mechanism used in many data structures. For instance, to store a list of items, we could use a contiguous array, but insertion into the middle of the contiguous array requires relocation of many items. Rather than store the collection in an array, it is common to store each item in a separate, noncontiguous piece of memory, which is allocated as the program runs. Along with each object is a link to the next object. This link is a pointer variable, because it stores a memory location of another object. This is the classic linked list that is discussed in more detail in Chapter 3.

To illustrate the operations that apply to pointers, we rewrite Figure 1.9 to dynamically allocate the IntCell. It must be emphasized that for a simple IntCell class, there is no good reason to write the C++ code this way. We do it only to illustrate dynamic memory allocation in a simple context. Later in the text, we will see more complicated classes, where this technique is useful and necessary. The new version is shown in Figure 1.11.

### Declaration

Line 3 illustrates the declaration of m. The * indicates that m is a pointer variable; it is allowed to point at an IntCell object. The value of m is the address of the object that it points at.

```
1 int main( )
2 {
3     IntCell *m;
4
5     m = new IntCell{ 0 };
6     m->write( 5 );
7     cout << "Cell contents: " << m->read( ) << endl;
8
9     delete m;
10    return 0;
11 }
```

Figure 1.11 Program that uses pointers to IntCell (there is no compelling reason to do this)

m is uninitialized at this point. In C++, no such check is performed to verify that m is assigned a value prior to being used (however, several vendors make products that do additional checks, including this one). The use of uninitialized pointers typically crashes programs, because they result in access of memory locations that do not exist. In general, it is a good idea to provide an initial value, either by combining lines 3 and 5, or by initializing m to the null pointer.

### Dynamic Object Creation

Line 5 illustrates how objects can be created dynamically. In C++ new returns a pointer to the newly created object. In C++ there are several ways to create an object using its zero-parameter constructor. The following would be legal:

```
m = new IntCell( ); // OK
m = new IntCell[ ]; // C++11
m = new IntCell; // Preferred in this text
```

We generally use the last form because of the problem illustrated by obj4 in Section 1.4.3.

### Garbage Collection and delete

In some languages, when an object is no longer referenced, it is subject to automatic garbage collection; the programmer does not have to worry about it. C++ does not have garbage collection. When an object that is allocated by new is no longer referenced, the delete operation must be applied to the object (through a pointer). Otherwise, the memory that it consumes is lost (until the program terminates). This is known as a memory leak. Memory leaks are, unfortunately, common occurrences in many C++ programs. Fortunately, many sources of memory leaks can be automatically removed with care. One important rule is to not use new when an automatic variable can be used instead. In the original program, the IntCell is not allocated by new but instead is allocated as a local variable. In that case, the memory for the IntCell is automatically reclaimed when the function in which it is declared returns. The delete operator is illustrated at line 9 of Figure 1.11.

### Assignment and Comparison of Pointers

Assignment and comparison of pointer variables in C++ is based on the value of the pointer, meaning the memory address that it stores. Thus two pointer variables are equal if they point at the same object. If they point at different objects, the pointer variables are not equal, even if the objects being pointed at are themselves equal. If lhs and rhs are pointer variables (of compatible types), then lhs==rhs makes lhs point at the same object that rhs points at.⁴

⁴ Throughout this text, we use lhs and rhs to signify left-hand side and right-hand side of a binary operator.

### Accessing Members of an Object through a Pointer

If a pointer variable points at a class type, then a (visible) member of the object being pointed at can be accessed via the -> operator. This is illustrated at lines 6 and 7 of Figure 1.11.

### Address-of Operator (&)

One important operator is the **address-of operator** &. This operator returns the memory location where an object resides and is useful for implementing an alias test that is discussed in Section 1.5.6.

### 1.5.2 Lvalues, Rvalues, and References

In addition to pointer types, C++ defines reference types. One of the major changes in C++11 is the creation of a new reference type, known as an rvalue reference. In order to discuss rvalue references, and the more standard value reference, we need to discuss the concept of lvalues and rvalues. Note that the precise rules are complex, and we provide a general description rather than focusing on the corner cases that are important in a language specification and for compiler writers.

An **lvalue** is an expression that identifies a non-temporary object. An **rvalue** is an expression that identifies a temporary object or is a value (such as a literal constant) not associated with any object.
As examples, consider the following:

```
vector<string> arr( 3 );
const int x = 2;
int y;
...
int z = x + y;
string str = "foo";
vector<string> *ptr = &arr;
```

With these declarations, arr, str, arr[x], &x, y, z, ptr, *ptr, (*ptr)[x] are all lvalues. Additionally, x is also an lvalue, although it is not a modifiable lvalue. As a general rule, if you have a name for a variable, it is an lvalue, regardless of whether it is modifiable.

For the above declarations 2, "foo", x*y, str.substr(0,1) are all rvalues. 2 and "foo" are rvalues because they are literals. Intuitively, x*y is an rvalue because its value is temporary; it is certainly not x or y, but it is stored somewhere prior to being assigned to z. Similar logic applies for str.substr(0,1).

Notice the consequence that there are some cases in which the result of a function call or operator call can be an lvalue (since *ptr and arr[x] generate lvalues) as does cin>>x>>y and others where it can be an rvalue, hence, the language syntax allows a function call or operator overload to specify this in the return type, and this aspect is discussed in Section 1.5.4. Intuitively, if the function call computes an expression whose value does not exist prior to the call and does not exist once the call is finished unless it is copied somewhere, it is likely to be an rvalue.

A reference type allows us to define a new name for an existing value. In classic C++, a reference can generally only be a name for an lvalue, since having a reference to a temporary would lead to the ability to access an object that has theoretically been declared as no longer needed, and thus may have had its resources reclaimed for another object. However, in C++11, we can have two types of references: lvalue references and rvalue references.
