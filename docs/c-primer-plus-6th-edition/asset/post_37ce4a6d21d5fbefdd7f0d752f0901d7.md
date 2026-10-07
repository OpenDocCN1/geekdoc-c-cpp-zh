
# Answers to Chapter Review for Chapter 14

```cpp
2. Gloam::Gloam(int g, const char * s) : glip(g), fb(s) { }
Gloam::Gloam(int g, const Frabious & fr) : glip(g), fb(fr) {
  // note: the above uses the default Frabious copy constructor
}
void Gloam::tell()
{
  fb.tell();
  cout << glip << endl;
}
```

```cpp
3. Gloam::Gloam(int g, const char * s) : glip(g), Frabious(s) { }
Gloam::Gloam(int g, const Frabious & fr) : glip(g), Frabious(fr) {
  // note: the above uses the default Frabious copy constructor
}
void Gloam::tell()
{
  Frabious::tell();
  cout << glip << endl;
}
```

```cpp
4. class Stack<Worker *> {
private:
  enum {MAX = 10}; // constant specific to class
  Worker * items[MAX]; // holds stack items
  int top; // index for top stack item
public:
  Stack();
  Boolean is();
  Boolean isfull();
  Boolean push(Worker * & item); // add item to stack
  Boolean pop(Worker * & item); // pop top into item
};
```

Listing 14.18 generates four templates: ArrayTP<int, 10>, ArrayTP<double, 10>, ArrayTP<int, 5>, and Array<int, 5, 10>.

6. If two lines of inheritance for a common ancestor, the class winds up having two copies of the ancestor's members. Making the ancestor class a virtual base class to its immediate descendants solves the problem.

# Answers to Chapter Review for Chapter 15

- 1. a. The friend declaration should be as follows:
  `friend class clasp;`
  b. This needs a forward declaration so that the compiler can interpret void:
  ```cpp
  void snip(muff &); // forward declaration
  class muff;
  class cuff {
  public:
      void snip(muff &) { ... }
      ...
  };
  class muff {
      friend void cuff::snip(muff &);
      ...
  };
  ```
  c. First, the cuff class declaration should precede the muff class so that the compiler can understand the term `cuff::snip()`. Second, the compiler needs a forward declaration of muff so that it can understand `snip(muff &)`:
  ```cpp
  class muff; // forward declaration
  class cuff {
  public:
      void snip(muff &) { ... }
      ...
  };
  class muff {
      friend void cuff::snip(muff &);
  };
  ```

- 2. For Class A to have a friend that is a member function of Class B, the B declaration must precede the A declaration. A forward declaration is not enough because it would tell A that B is a class, but it wouldn't reveal the names of the class members. Similarly, if B has a friend that is a member function of A, the complete A declaration must precede the B declaration. These two requirements are mutually exclusive.

- 3. The only access to class is through its public interface, which means the only thing you can do with a Sauce object is the constructor to create one. The other members and sugar are private by default.

- 4. Suppose the function f1() calls the function f2(). A return statement in f2() causes program execution to resume at the next statement following the f2() function call in f1(). A throw statement causes the program to back up through the current function sequence of calls until it finds a try block that directly or indirectly calls the f2(). This might be in f1() or in a function called f1(), and so on. Once, execution goes to the next matching catch block, not to the first statement after the function call.

- 5. You should arrange the catch blocks in order, from most derived to least derived.

- 6. For Sample #1, if the condition is true, pg points to a Superb object or to an object of any class descended from Superb. In particular, it is also true if pg points to a Magnificent object. In Sample #2, if the condition is true only for objects derived from Superb.

- 7. The dynamic_cast operator only allows upcasting in a class hierarchy, whereas a static_cast operator allows both upcasting and downcasting. The static_cast operator also allows conversions from enumeration types to integer types, and vice versa, between various numeric types.

# Answers to Chapter Review for Chapter 16

- 1. #include <string>
using namespace std;
class RQ1
private:
    string st; // a string object
public:
    RQ1() : st("") {}
    RQ1(const char * s) : st(s) {}
    ~RQ1() {};
    // more stuff
};

The explicit copy constructor, destructor, and assignment operator are no longer needed because the string object provides its own memory management.

- 2. You can assign one string object to another. A string object provides its own memory management that you normally don't have to worry about exceeding the capacity of its holder.

- 3. #include <string>
#include <ctype>
using namespace std;
void ToUpper(string & str)
```cpp
{
  for (int i = 0; i < str.size(); i++)
    str[i] = toupper(str[i]);
}
```
*(Note: The OCR text became highly garbled in this section; I have preserved the structure while cleaning up logical flow where possible based on common C++ patterns.)*

- 5. ... 
- 6. ...
- 7. ...
- 8. ...
- 9. ...
- 10. The sort() function and the random_shuffle() function require a random access iterator, whereas a list has a bidirectional iterator. You could copy the list to a vector, shuffle the vector, and copy the results back to the list.

# Answers to Chapter Review for Chapter 17

- 1. The iostream file defines the classes, constants, and manipulators used to manage input and output. These objects manage the streams and buffers the file also contains standard objects (cin, cout, cerr, and clog their wide-character equivalents) used to handle standard input and output streams connected to every program.

# Answers to Chapter Review for Chapter 17

2. Keyboard entry generates a series of characters. Typing 121 generates three characters, each represented by a 1-byte code. If the value is to be stored as type int, these three characters have to be converted to a single binary representation of the value 121.

3. By default, both the standard output and the standard error send output to standard device, typically a monitor. If you have the operating system redirect output to a file, however, the standard output connects to the file instead of the screen, the standard error continues to be connected to the screen.

4. The ostream class defines a version of the operator<< function for each basic C++ type. The compiler interprets an expression like
```cpp
cout << spot
```
as the following:
```cpp
cout.operator<<(spot)
```
It can then match this method call to the function prototype that has the same argument type.

5. You can concatenate output methods that return type ostream &. This causes the invoking of a method with object to return that object. The returned object can then invoke the next method in a sequence.
