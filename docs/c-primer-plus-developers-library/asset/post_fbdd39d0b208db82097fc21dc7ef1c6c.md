
deletes the temporary object returned by allcaps(). (A really uninspired compiler could even copy temp to a temporary return object, delete temp, and then delete the return object.) The main point is that a lot of effort is wasted here. Because the temporary object is deleted, wouldn't it be better if the compiler could just transfer ownership of the data to vstr_copy2? That is, instead of copying 20,000,000 characters to a new location and then deleting the old location, just leave the characters in place and attach the vstr_copy2 label to them. This would be similar to what happens when you move a file from one directory to another: The actual file stays where it is on the hard drive, and just the bookkeeping is altered. Such an approach is called move semantics. Somewhat paradoxically, move semantics actually avoids moving the primary data; it just adjusts the bookkeeping.

To implement move semantics, we need a way to let the compiler know when it needs to do a real copy and when it doesn't. Here's where the rvalue reference comes into play. We can define two constructors. One, the regular copy constructor, can use the usual const lvalue reference as a parameter. This reference will bind to lvalue arguments, such as vstr in statement #1. The other, called a move constructor, can use an rvalue reference, and it can bind to rvalue arguments, such as the return value of allcaps(vstr) in statement #2. The copy constructor can do the usual deep copy, while the move constructor can just adjust the bookkeeping. A move constructor may alter its argument in the process of transferring ownership to a new object, and this implies that an rvalue reference parameter should not be const.

## A Move Example

Let's look at an example to see how move semantics and rvalue references work. Listing 18.2 defines and uses the Useless class, which incorporates dynamic memory allocation, a regular copy constructor, and a move constructor, which uses move semantics and an rvalue reference. In order to illustrate the processes involved, the constructors and destructor are unusually verbose, and the class uses a static variable to keep track of the number of objects. Also some important methods, such as the assignment operator, are omitted. (Despite these omissions, the Useless class should not be confused with the eco-friendly Use_Less class.)

Listing 18.2  useless.cpp

```cpp
// useless.cpp -- an otherwise useless class with move semantics
#include <iostream>
using namespace std;

// interface
class Useless
{
private:
    int n;          // number of elements
    char * pc;      // pointer to data
    static int ct;  // number of objects
    void ShowObject() const;
public:
    Useless();
    explicit Useless(int k);
    Useless(int k, char ch);
    Useless(const Useless & f);     // regular copy constructor
    Useless(Useless && f);          // move constructor
    ~Useless();
    Useless operator+(const Useless & f)const;
    // need operator= in copy and move versions
    void ShowData() const;
};


// implementation
int Useless::ct = 0;

Useless::Useless()
{
    ++ct;
    n = 0;
    pc = nullptr;
    cout << "default constructor called; number of objects: " << ct << endl;
    ShowObject();
}

Useless::Useless(int k) : n(k)
{
    ++ct;
    cout << "int constructor called; number of objects: " << ct << endl;
    pc = new char[n];
    ShowObject();
}

Useless::Useless(int k, char ch) : n(k)
{
    ++ct;
    cout << "int, char constructor called; number of objects: " << ct
         << endl;
    pc = new char[n];
    for (int i = 0; i < n; i++)
        pc[i] = ch;
    ShowObject();
}

Useless::Useless(const Useless & f) : n(f.n)
{
    ++ct;
    cout << "copy const called; number of objects: " << ct << endl;
    pc = new char[n];
    for (int i = 0; i < n; i++)
        pc[i] = f.pc[i];
    ShowObject();
}

Useless::Useless(Useless && f): n(f.n)
{
    ++ct;
    cout << "move constructor called; number of objects: " << ct << endl;
    pc = f.pc;       // steal address
    f.pc = nullptr;  // give old object nothing in return
    f.n = 0;
    ShowObject();
}

Useless::~Useless()
{
    cout << "destructor called; objects left: " << --ct << endl;
    cout << "deleted object:\n";
    ShowObject();
    delete [] pc;
}

Useless Useless::operator+(const Useless & f)const
{
    cout << "Entering operator+()\n";
    Useless temp = Useless(n + f.n);
    for (int i = 0; i < n; i++)
        temp.pc[i] = pc[i];
    for (int i = n; i < temp.n; i++)
        temp.pc[i] = f.pc[i - n];
    cout << "temp object:\n";
    cout << "Leaving operator+()\n";
    return temp;
}

void Useless::ShowObject() const
{
    cout << "Number of elements: " << n;
    cout << " Data address: " << (void *) pc << endl;
}

void Useless::ShowData() const
{
    if (n == 0)
        cout << "(object empty)";
    else
        for (int i = 0; i < n; i++)
            cout << pc[i];

    cout << endl;
}

// application
int main()
{
    {
        Useless one(10, 'x');
        Useless two = one;          // calls copy constructor
        Useless three(20, 'o');
        Useless four (one + three);  // calls operator+(), move constructor
        cout << "object one: ";
        one.ShowData();
        cout << "object two: ";
        two.ShowData();
        cout << "object three: ";
        three.ShowData();
        cout << "object four: ";
        four.ShowData();
    }
}
```

The crucial definitions are those of the two copy/move constructors. First, shorn of the output statements, here is the copy constructor:

```cpp
Useless::Useless(const Useless & f): n(f.n)
{
    ++ct;
    pc = new char[n];
    for (int i = 0; i < n; i++)
        pc[i] = f.pc[i];
}
```

It does the usual deep copy, and it is the constructor that's used by the following statement:

```cpp
Useless two = one;          // calls copy constructor
```

The reference f refers to the lvalue object one.

Next, again shorn of the output statements, here is the move constructor:

```cpp
Useless::Useless(Useless && f): n(f.n)
{
    ++ct;
    pc = f.pc;       // steal address
    f.pc = nullptr;  // give old object nothing in return
    f.n = 0;
}
```

It takes ownership of the existing data by setting pc to point to the data. At this time, both pc and f.pc point to the same data. This would be awkward when the destructors are called, because a program shouldn't call delete [] twice for the same address. To avoid this problem, the constructor then sets the original pointer to the null pointer because it is not an error to apply delete [] to the null pointer. This appropriation of ownership often is termed pilfering. The code also sets the element count in the original object to 0. This isn't necessary, but it makes the output for our example look more self-consistent. Note that the changes to the f object require not using const in the parameter declaration.

It is this constructor that is used in the following statement:

```cpp
Useless four (one + three);   // calls move constructor
```

The expression one + three invokes Useless::operator+(), and the rvalue reference f binds to the rvalue temporary object returned by the method.

Here's the output when the program was compiled with Microsoft Visual C++ 2010:

```
int, char constructor called; number of objects: 1
Number of elements: 10 Data address: 006F4B68
copy const called; number of objects: 2
Number of elements: 10 Data address: 006F4BB0
int, char constructor called; number of objects: 3
Number of elements: 20 Data address: 006F4B98
Entering operator+()
int constructor called; number of objects: 4
Number of elements: 30 Data address: 006F4C48
temp object:
Leaving operator+()
move constructor called; number of objects: 5
Number of elements: 30 Data address: 006F4C48
destructor called; objects left: 4
deleted object:
Number of elements: 0 Data address: 00000000
object one: xxxxxxxxxx
object two: xxxxxxxxxx
object three: oooooooooooooooooooooooo
object four: xxxxxxxxxxxxxxxxxxxxxxxxxxxxx
destructor called; objects left: 3
```
