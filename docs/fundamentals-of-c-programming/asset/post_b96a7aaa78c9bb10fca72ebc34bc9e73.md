

```
// The constructor makes an initially empty list.
// The list is empty when head and tail are null.
// The list's size initially is zero.
IntList4::IntList4(): head(nullptr), tail(nullptr), len(0) {}
```

```
// Copy constructor makes a copy of the other object's list
IntList4::IntList4(const IntList4& other) {
// Walk through other's list inserting each of its elements
// into this list
for (auto cursor = other.head; cursor; cursor = cursor->next)
insert(cursor->data);
}
```

```
// Assignment operator
IntList4 IntList4::operator=(const IntList4& other) {
// Make a local, temporary copy of other
IntList4 temp(other);
// Exchange the head and tail pointers and len from this list
// with those of the new, temporary list
std::swap(head, temp.head);
std::swap(tail, temp.tail);
std::swap(len, temp.len);
// The temporary list now points to this list's original contents,
// and this list now points to the copy of other's list
// The temporary list will be destroyed when this constructor returns
return *this;
}
```

```
// The destructor deallocates the memory held by the list
IntList4::~IntList4() { clear(); }
```

```
// Inserts n onto the back of the list.
// n is the element to insert.
void IntList4::insert(int n) {
// Make a node for the new element
IntList4::Node* new_node = new Node(n);
if (tail) { // Is tail non-null?
tail->next = new_node; // Link the new node onto the back
tail = new_node; // The new node is the new tail of the list
}
else // List is empty, so make head and tail point to new node
head = tail = new_node;
len++; // List now has one more element
}
```

```
// Prints the contents of the linked list of integers.
void IntList4::print() const {
for (auto cursor = head; cursor; cursor = cursor->next)
std::cout << cursor->data << ' ';
std::cout << '\n';
}
```

```
// Returns the length of the linked list.
int IntList4::length() const {
return len;
}
```

Figure 18.6. An annotated output of Listing 18.13 (listassign.cpp) updated to use our IntList4 class. Examine carefully the node memory addresses (in parentheses) to convince yourself that the implementation of correct copy constructor, assignment operator, and destructor for the class solved the aliasing, memory leak, and undefined behavior problems.

![](img/e84ad11adb18201d71595b31ce6c9eff_588_0.png)

```
// Removes all the elements in the linked list.
void IntList4::clear() {
    auto cursor = head;
    while (cursor) {
        auto temp = cursor;
        cursor = cursor->next;
        delete temp;
    }
    head = tail = nullptr; // Null head signifies list is empty
    len = 0;
}
```

Figure 18.6 provides an annotated output of Listing 18.13 (listassign.cpp) updated to use our IntList4 class.

The output demonstrates that assignment now works correctly for our linked list objects. Correctly implementing the copy constructor, assignment operator, and destructor for the IntList4 class solved the aliasing, memory leak, and undefined behavior concerns.

The copy constructor, assignment operator, and destructor have a special relationship in C++. These three methods are involved in the Rule of Three. The Rule of Three is this: If a class designer feels the need to add a copy constructor, assignment operator, and/or destructor to a class, the class should have all three methods. Said another way, it almost always is a mistake to have just one or two of these special methods defined for a class without including all three.

The Rule of Three is a design guideline; it is not requirement of the C++ language that the compiler enforces. Consider why the rule exists. If an object must be guaranteed to perform some action at the end of its existence and failure to do so would result in undesirable consequences as the program continues to execute, the object's class must contain a destructor. This essential action usually involves releasing some resource it owns. If the destructor is responsible for releasing a resource, the copy constructor must somehow acquire a resource that is in some way related to the resource of an existing object. The assignment operator must both release an owned resource and acquire a resource related to the resource of an existing object. What if you leave out one of the three?

- If you omit the destructor, the default destructor does no resource clean up. Objects can acquire resources through copy construction and assignment but cannot release them. Most resources (like memory) are finite, so lack of an appropriate destructor will limit the number objects available to the executing application.
- If you omit the copy constructor, the default copy constructor will copy the bits of the existing object into the new object. This means the copy-constructed object will have the exact resources managed by another object. The destruction of exactly one of the objects will release the resources held by the other object. The non-destroyed object then will not have access to the resources it needs to function.
- If you omit the assignment operator, the default assignment will copy the bits of one existing object into another existing object. This means the assigned-to object will have the exact resources managed by another object. It also means that the resources the assigned-to object originally held are not reclaimed. The destruction of exactly one of the objects will release the resources held by the other object. The non-destroyed object then will not have access to the resources it needs to function.

In sum, you should have a very good reason for designing a class that violates the Rule of Three.

## 18.5 Rvalue References

Consider the following code fragment:

```cpp
int x = 5, y;
y = x + 2;
```

In the assignment statement

```cpp
y = x + 2;
```

The variable y is known as an lvalue. The l in lvalue stands for left, as y can appear all by itself on the left side or right side of the assignment operator. The expression x + 2 is classified as an rvalue, since it can appear only on the right side of the assignment operator but cannot appear on the left side; for example, the following statement is illegal:

```cpp
x + 2 = y; // Illegal!
```

The expression x + 2 represents a temporary value, as it has meaning and existence only during the execution of the statement in which it appears. The executing program stores the result of the computation of x + 2 temporarily in memory, but the program ordinarily cannot reference that memory after the statement finishes. The term temporary is appropriate, as the program may reuse that same memory for other purposes after the statement executes.

Consider the following variable declarations:

```cpp
int x = 5;
int& r = x + 3; // Illegal!
```

The second declaration is illegal; C++ does not allow us to assign a temporary to a reference variable. In this case the variable r would be an alias for a quantity that ceases to exist immediately after the statement executes. The variable r, however, would continue to exist, but it would be aliasing any valid quantity.

C++ does permit us to make a const reference to a temporary. The following code fragment is legal:

```cpp
int x = 5;
const int& cr = x + 3; // Legal
```

The const reference places the value of the temporary into a memory location referenced via cr. The temporary's value persists until cr goes out of scope. In this case cr behaves as if it were simply a const int.

Next, consider the following function definition:

```cpp
int f(int n) {
    return 10 * n;
}
```

In the following statement:

```cpp
std::cout << f(x + 2) << '\n';
```

the actual parameter is a temporary value passed to the function f. Everything works as expected because the executing program copies the temporary's value to the formal parameter n in this pass by value example.

Now consider a similar but slightly different function definition:

```cpp
int g(int& n) {
    return 10 * n;
}
```

The following statement is illegal:

```cpp
std::cout << g(x + 2) << '\n';
```

The function g accepts a reference to a variable, but the caller is attempting to pass a temporary. Once function g begins executing, the memory reserved for the original temporary is invalid, so the compiler rightly does not permit this.

As with the simple declarations we saw above, given function h:

```cpp
int h(const int& n) {
    return 10 * n;
}
```

the following statement is perfectly acceptable:

```cpp
std::cout << h(x + 2) << '\n';
```

