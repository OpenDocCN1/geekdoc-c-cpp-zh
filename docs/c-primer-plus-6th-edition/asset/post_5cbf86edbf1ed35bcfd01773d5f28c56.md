
// below, rx refers to a temporary variable initialized to 21
int k = twice(21);

So in the Useless case, the formal parameter f will be initialized to a temporary object's initialized to the return value of operator+(). Here is an excerpt from the result of using an old compiler with Listing 18.2 and omitting the move constructor:

```
Entering operator+
int constructor called; number of objects: 4
Number of elements: 30 Data address: 01C337C4
temp object:
Leaving operator+()
copy const called; number of objects: 5
Number of elements: 30 Data address: 01C337E8
destructor called; objects left: 4
deleted object:
Number of elements: 30 Data address: 01C337C4
copy const called; number of objects: 5
Number of elements: 30 Data address: 01C337C4
destructor called; objects left: 4
deleted object:
Number of elements: 30 Data address: 01C337E8
```

First, within the Useless::operator() method, a constructor creates temp, allocating storage for 30 elements at location 01C337C4. Then the copy constructor creates a temporary copy to f will refer, copying the information to location 01C337E8. Next, temp, which uses location 01C337C4, gets deleted. A new object, for is constructed, reusing the free memory at 01C337C4. Then the temporary object, which used location 01C337E8, gets deleted. So three complete objects are constructed, and two of them were destroyed. This is the sort of extra work semantics are meant to eliminate.

As the g++ example shows, an optimizing compiler might eliminate extra copying on its own, but using an rvalue reference lets the programmer dictate move semantics for appropriate.

## Assignment

The same considerations that make move semantics appropriate for constructors make them appropriate for assignment. Here, for example, how you could code the copy assignment and move assignment operators for the Useless class:

```
Useless & Useless::operator=(const Useless & f) // copy assignment
{
  if (this == &f)
```

```
return *this;
delete [] pc;
n = f.n;
pc = new char[n];
for (int i = 0; i < n; i++)
pc[i] = f.pc[i];
return *this;

```

```
Useless & Useless::operator=(Useless && f) // move assignment
{
    if (this == &f)
        return *this;
    delete [] pc;
    n = f.n;
    pc = f.pc;
    f.n = 0;
    f.pc = nullptr;
    return *this;
}
```

The copy assignment operator follows the usual pattern given in Chapter 12. The move assignment operator deletes the original data in the target and pilfers the source object. It's important that only one pointer points to the data, so the move resets the pointer in the source object to the null pointer.

As with the move constructor, the move assignment operator parameter is not a const reference because the method alters the source object.

## Forcing a Move

Move constructors and move assignment operators work with rvalues. What if you want to use them with lvalues? For instance, a program could analyze an array of some sort of candidate objects, select one object for further use, and discard the array. It would be convenient if you could use a move constructor or a move assignment operator to preserve the selected object. However, suppose you tried the following:

```
Useless choices[10];
Useless best;
int pick;
... // select one object, set pick to index
best = choices[pick];
```

The choices[pick] object is an lvalue, so the assignment statement would use the copy assignment operator, not the move operator. But if you could make choices[pick] look like an rvalue, then the move assignment operator would be used. This can be done by using the static_cast<Useless&&> operator to cast the object to type Useless&&. Useless & C++11 provides a simpler way to do this—use the std::move() function,

which is declared in the utility header file. Listing 18.3 illustrates this technique. It adds
verse versions of the assignment operators to the Useless class while silencing the pre-
viously verbose constructors and destructor.

## Listing 18.3 stdmove.cpp

```
// stdmove.cpp -- using std::move()
#include <iostream>
#include <utility>

// interface
class Useless
{
private:
    int n;               // number of elements
    char * pc;           // pointer to data
    static int ct;        // number of objects
    void ShowObject() const;
public:
    Useless();
    explicit Useless(int k);
    Useless(int k, char ch);
    Useless(const Useless & f); // regular copy constructor
    Useless(Useless && f);      // move constructor
    ~Useless();
    Useless operator=(const Useless & f) const;
    Useless & operator=(const Useless & f); // copy assignment
    Useless & operator=(Useless && f);      // move assignment
    void ShowData() const;
};

// implementation
int Useless::ct = 0;

Useless::Useless()
{
    ++ct;
    n = 0;
    pc = nullptr;
}

Useless::Useless(int k) : n(k)
{
    ++ct;
    pc = new char[n];
}
```

## Move Semantics and the Rvalue Reference 1175

```
Useless::Useless(int k, char ch) : n(k)
{
  ++ct;
  pc = new char[n];
  for (int i = 0; i < n; i++)
    pc[i] = ch;
}
```

```
Useless::Useless(const Useless & f) : n(f.n)
{
  ++ct;
  pc = new char[n];
  for (int i = 0; i < n; i++)
    pc[i] = f.pc[i];
}
```

```
Useless::Useless(Useless && f) : n(f.n)
{
  ++ct;
  pc = f.pc; // steal address
  f.pc = nullptr; // give old object nothing in return
  f.n = 0;
}
```

```
Useless::~Useless()
{
  delete [] pc;
}
```

```
Useless & Useless::operator=(const Useless & f) // copy assignment
{
  std::cout << "copy assignment operator called:\n";
  if (this != &f)
    return *this;
  delete [] pc;
  n = f.n;
  pc = new char[n];
  for (int i = 0; i < n; i++)
    pc[i] = f.pc[i];
  return *this;
}
```

```
Useless & Useless::operator=(Useless && f) // move assignment
{
  std::cout << "move assignment operator called:\n";
  if (this == &f)
```

```
return *this;
delete [] pc;
n = f.n;
pc = f.pc;
f.n = 0;
f.pc = nullptr;
return *this;
}
```

```
Useless Useless::operator+(const Useless & f) const
{
    Useless temp = Useless(n + f.n);
    for (int i = 0; i < n; i++)
        temp.pc[i] = pc[i];
    for (int i = n; i < temp.n; i++)
        temp.pc[i] = f.pc[i - n];
    return temp;
}
```

```
Useless Useless::ShowObject() const
{
    std::cout << "Number of elements: " << n;
    std::cout << " Data address: " << (void*) pc << std::endl;
```

```
Useless Useless::ShowData() const
{
    if (n == 0)
        std::cout << "(object empty)";
    else
        for (int i = 0; i < n; i++)
            std::cout << pc[i];
    std::cout << std::endl;
}
```

```
// application
int main()
{
    using std::cout;
    Useless one(10, 'x');
    Useless two = one + one;    // calls move constructor
    cout << "object one: " << one;
    one.ShowData();
    cout << "object two: " << two;
    two.ShowData();
}
```

## Move Semantics and the Rvalue Reference 1177

```
Useless three, four;
cout << "three = one\n";
three = one;                  // automatic copy assignment
cout << "now object three = ";
three.ShowData();
cout << "and object one = ";
one.ShowData();
cout << "four = one + two\n";
four = one + two;              // automatic move assignment
cout << "now object four = ";
four.ShowData();
cout << "four = move(one)\n";
four = std::move(one);        // forced move assignment
cout << "now object four = ";
four.ShowData();
cout << "and object one = ";
one.ShowData();
}
```

Here is a sample run:

```
object one: xxxxxxxxxx
object two: xxxxxxxxxxxxxxxxxx
three = one
copy assignment operator called:
now object three = xxxxxxxxxx
and object one = xxxxxxxxxx
four = one + two
move assignment operator called:
now object four = xxxxxxxxxxxxxxxxxxxxxxxxxx
four = move(one)
move assignment operator called:
now object four = xxxxxxxxxx
and object one = (object empty)
```

As you can see, assigning one to three invokes copy assignment, but assigning move(one) to four invokes move assignment.
You should realize that the std::move() function doesn't necessarily produce a move operation. Suppose, for instance, that Chunk is a class with private data and that we have the following code:

```
Chunk one;
...
Chunk two;
two = std::move(one); // move semantics
```
