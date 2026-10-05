
# 16.7 SUMMARY

```cpp
else if (r == 9995)
   count9995++; // 9,995 generated, so count it
{
   // Display the number of times the program generated 5 and 9,995
   cout << "Trial " << setw(2) << trial << " 5: " << setw(6) << count5
     << "9995: " << setw(6) << count9995 << endl;
   total5 += count5; // Accumulate the counts to
   total9995 += count9995; // average time at the end
}
cout << "--------------------------------" << endl;
cout << "Averages for " << NUMBER_OF_TRIALS << " trials: 5: "
     << setw(6) << total5 / NUMBER_OF_TRIALS << " 9995: "
     << setw(6) << total9995 / NUMBER_OF_TRIALS << endl;
```

Note that in Listing 16.13 (uniformrandom.cpp), the statement

```
int r = rand();
```

is not a claim to our familiar std::rand; rather, rand is a UniformRandomGenerator object, and the statement is invoking its operator method.

# 16.7 Summary

- The object-oriented features of C++ allow designers to design a variety of useful classes for programming tasks.
- Sophisticated computation can be packaged within objects that are relatively easy for clients to use.

# 16.8 Exercises

- 1. Recall the insert method from Listing 16.7 (intlist.cpp) and consider the following insert function contains only a couple of minor modifications to the original version:

```cpp
IntList::Node *IntList::insert(Node *p, int n) {
   // Check that we are not at the end of the list and
   // that the current list element is less than the new
   // item to add.
   if (p && p->data < n)
      p->next = insert(p->next, n); // Insert into rest of list
   else {
      Node *temp = new Node;
      temp->data = n;
      temp->next = p;
      p = temp;
   }
   return p;
}
```

- (a) Without executing the code, can you predict how this new version behaves differently, if at all, from the original version?
(b) Replace the *insert* function in Listing 16.7 (intlist.cpp) with this new version to check your prediction. Can you explain why this new *insert* function behaves the way it does?

# Chapter 17

# Inheritance and Polymorphism

In Chapter 16 we saw how it is possible to design classes from which clients can produce objects that exhibit somewhat sophisticated behavior. The Rational, Stopwatch, LinkedList, and Tester classes were each built from scratch. C++ provides a way to create a class from an existing class by a process known as inheritance. Through this process the new class inherits all the characteristics of the existing class, and the class developer can extend and customize the inherited functionality as well as add new features.

# 17.1 I/O Stream Inheritance

Recall from Section 13.3 that writing to a file is almost as easy as printing on the screen. Once an ofstream object is set up, we can use the << operator in the same way we use it with the cout:

```cpp
ofstream fout("myfile.dat");
int x = 10;
if (fout.good()) { // Make sure the file was opened properly
    fout << "x = " << x << endl;
    fout.close();
}
else
    cout << "Unable to write to the file \"myfile.dat\"" << endl;
```

Section 15.6 shows how operator<< may be overloaded for a programmer-defined type. For a type of vectors we can use the function

```cpp
ostream operator<<(ostream& os, const vector<int>& vec) {
    os << "{";
    int n = vec.size();
    if (n > 0) { // Is the vector non-empty?
        os << vec[0]; // Send first element to the stream
        for (int i = 1; i < n; i++)
            os << ", " << vec[i]; // Send remaining elements
    }
    os << "}";
    return os;
}
```

# 17.1 I/O STREAM INHERITANCE

Can we easily adapt our << operator so that we can use it with ofstream objects?

The answer, perhaps surprisingly, is not that we do not have to adapt our operator<< function; it works as with ofstream objects. How can this be, since the count object has type ofstream is not the same class as ofstream?

C++ allows some automatic conversions in the numeric types; for example, an int is widened to a double, and a double is truncated to an int. bool and ints are freely interconvertible. These types are built into the library, so standards apply. When it comes to programmer-defined types, the compiler is unable to automatically generate code to convert one to another. Most of the time it would make no sense to do so—imaginary attempting to convert an object of type Stopwatch(16) to an object of type Tester(16).

So, how is that an object of type ofstream be automatically converted to an object of type ostream? You might think that is because both are part of the standard library, so the conversion has been programmed into them. The conversion takes place! Any object of type ofstream object is automatically treated as if it were an ostream object because of the ostream and ofstream classes are in a special relation. The ofstream class is derived from the ostream class. We may say that ostream is the base class and ofstream is the derived class. Sometimes the term superclass is used instead of subclass. The base/derived class terminology is used interchangeably with super/subclass, although the C++ community tends to prefer the base/derived over super/subclass. The process is known as inheritance because the derived class inherits the characteristics of its base class. The terms derivation, subclassing and specialization are used sometimes in place of the term inheritance.

As a consequence of the derivation process, an instance of the derived class can be treated as if it were an instance of the base class. Listing 17.1 (printstreams.cpp) shows how a function can process instances of two different classes by inheritance.

Listing 17.1: printstreams.cpp

```cpp
#include <fstream>

using namespace std;

void print(ostream& os, int n) {
    os.width(10); // Right filled in 10 spaces
    os.fill('*'); // Fill character is *
    os << n << endl;
}

int main() {
    // Pretty print to screen
    print(cout, 35);

    // Pretty print to text file
    ofstream out("temp.data");
    if (out.good()) {
        print(out, 36);
    }
    out.close();
}
```

# 17.2 INHERITANCE MECHANICS

Observe that the print function in Listing 17.1 (streams.cpp) expects a client to pass an ostream reference as the first parameter, but the main function can send both ostream and ofstream object references with equal ease.

This ability to allow a subclass object to be used in any context that expects a superclass object is known as the Liskov Substitution Principle, after computer scientist Barbara Liskov.

The term has a special meaning in the context of inheritance. Suppose we have class B and class D derived from B. B is the base class and D is the derived class. Since the... [Note: The OCR text seems to be fragmented/duplicated in the later sections, but based on the provided input, the logic follows the explanation of inheritance where a derived class (D) can be treated as the base class (B).]
