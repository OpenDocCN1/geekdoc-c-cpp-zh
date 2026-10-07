
# Smart Pointer Template Classes 977

You may be wondering how unique_ptr, unlike auto_ptr, is able to discriminate between safe and possibly unsafe. The answer is that it uses the C++11 additions of move constructors and rvalue references, as discussed in Chapter 18.
Also unique_ptr has another advantage over auto_ptr. It has the variant that can be used with arrays. Remember, you must pair delete with new and delete [] with new []. The auto_ptr template uses delete, not delete [], so it can only be used with new, not with new []. But unique_ptr has new[], delete [] version:

```
std::unique_ptr<double> _pda(new double(5)); // will use delete
```

## Caution

You should use an auto_ptr or shared_ptr object only for memory allocated by new, not for memory allocated by new []. You should not use auto_ptr, shared_ptr, or unique_ptr for memory not allocated via new [], or in the case of unique_ptr, via new or new [].

## Selecting a Smart Pointer

Which pointer type should you use? The program uses more than one pointer to an object, shared_ptr is your choice. For instance, you may have an array of pointers and some auxiliary pointers to identify particular elements, such as the largest and the smallest. Or you could have two kinds of objects that contain pointers to the same object. Or you might have a STL of pointers. Many of the STL algorithms include copy or assignment operations that will work with shared_ptr but not with unique_ptr (you'll get a compiler warning) or auto_ptr (you'll get undefined behavior). If your compiler doesn't offer shared_ptr, you can get a version from the Boost library.
If the program doesn't need multiple pointers to the same object, unique_ptr works. It's a good choice for the return type for a function that returns a pointer to memory allocated by new. That way, ownership is transferred to the unique_ptr assigned the return value, and smart pointer takes the responsibility of calling delete. You can store unique_ptr objects in a STL container providing you don't invoke methods or algorithms, such as sort (), that copy or assign unique_ptr to another. For example, assuming the proper inclusion and using statements, code fragments like the following could be used in a program:

```
unique_ptr<int> make_int(int n)
{
    return unique_ptr<int>(new int(n));
}
void show(unique_ptr<int>& pi) // pass by reference
{
    cout << *pi << ' ';
}
int main()
{
    
```
```
vector<unique_ptr<int>> vp(size);
for (int i = 0; i < vp.size(); i++)
  vp[i] = make_int(rand() % 1000); // copy transfer unique_ptr
  vp.push_back(make_int(rand() % 1000)); // ok because arg is temporary
  for_each(vp.begin(), vp.end(), {});    // use for_each()
```

The call to push_back() works because it passes a temporary unique_ptr to be assigned to a unique_ptr. Also note the for_each() statement would fail if show were passed an object by value instead of by reference then it would be necessary to initialize pi to a nontemporary unique_ptr from vp, which isn't allowed. As mentioned before, the compiler will catch attempts to use unique_ptr inappropriately.

You can assign a unique_ptr to shared_ptr under the same conditions that you can assign one shared_ptr to another—the source has be an rvalue. As previously, in the following code make_int() is a function with a unique_ptr<int> return type:

```
unique_ptr<int> make_int(rand() % 1000); // ok
shared_ptr<int> spp(pup); // not allowed, pup an lvalue
shared_ptr<int> spr(make_int(rand() % 1000)); // ok
```

The shared_ptr template includes an explicit constructor for converting a unique_ptr to a shared_ptr. The shared_ptr takes ownership of the object previously owned by the unique_ptr. If you use auto instead of unique_ptr, but the latter is preferred. If your compiler doesn't provide unique_ptr, you might consider the BOOST library scoped_ptr, which is similar.

# The Standard Template Library

The STL provides a collection of templates representing containers, iterators, function objects, and algorithms. A container is a unit, like an array, that can hold several values. STL containers are homogeneous; that, they hold values of the same kind. Algorithms are recipes for accomplishing particular tasks, such as sorting an array or finding a value in a list. Iterators are objects that you move through a container as pointers let you move through an array; they are generalizations of pointers. Function objects are objects that can act like functions; they can be class or function pointers (including function names as function name acts as a pointer). The STL lets you construct a variety of containers, including arrays, queues, and lists, which lets you perform a variety of operations, including searching, sorting, and matching.

Alex Stepan and Meng Lee developed STL at Hewlett-Packard, releasing the implementation in 1994. The ISO/ANSI C++ committee voted to incorporate it as a part of the C++ Standard. The STL is not an example of object-oriented programming. Instead, it represents a different programming paradigm called generic programming. This makes STL interesting in terms of what it does and in terms of its approach.

The Standard Template Library 979

There's too much information about the STL to present in a single chapter, so we'll look at some representative examples and examine the spirit of the generic programming approach. We'll begin looking at a few specific examples. Then, when you have hands-on appreciation for comparators, iterators, and algorithms, we'll look at the underlying design philosophy and then take an overview of the whole STL. Appendix G," STL Methods and Functions," summarizes the various STL methods and functions.

# The vector Template Class

Chapter 4 touched briefly on the vector class. We'll look more closely at it now. In computing, the term vector corresponds to an array rather than the mathematical vector discussed in Chapter 11, "Working with Classes." (Mathematically, an N-dimensional mathematical vector can be represented by a set of N components, in that aspect, a mathematical vector has additional properties, such as inner and outer products, that a computer vector doesn't necessarily have.) A computing-style vector holds a set of values that can be accessed randomly. That is, you can use an index to access the 10th element of a vector without having to access the preceding 9 elements of the varlay and ArrayFP classes introduced in Chapter 14 and to those of the array class introduced in Chapter 4. That is, you could create a vector object, use one vector to another, and use the [] operator to access vector elements. To make the class generic, you make it a template. That's what the STL does, defining a template in the vector (formerly vector.h) header file.

To create a vector template object, you use the usual <type> notation to indicate the type to be used. Also the vector template uses dynamic memory allocation, and you can use an initialization argument to indicate how many vector elements you want:

```
#include vector
using namespace std;
vector<int> ratings(5); // a vector of 5 ints
int n;
cin >> n;
vector<double> scores(n); // a vector of n doubles
```

After you create a vector object, operator overloading for [] makes it possible to use the usual array notation for individual elements: ratings[0] = 9; for (int i = 0; i < n; i++) cout << scores[i] << endl;

# Allocators Again

Like the string class, the various STL container templates take an optional template argument that specifies which allocator object to use to manage memory. For example, the vector template begins like this:

template <class T, class Allocator = allocator<T> >
class vector {

If you omit a value for this template argument, the container template uses the
allocator<T> class by default. This class uses new and delete.

Listing 16.7 uses this class in an demanding application. This particular program cre-
ates vector objects, the one int specialization and one string specialization; each
has five elements.

# Listing 16.7 vect1.cpp

```
// vect1.cpp -- introducing the vector template
#include <iostream>
#include <string>
#include <vector>

const int NUM = 5;
int main()
{
  using std::vector;
  using std::string;
  using std::cin;
  using std::cout;
  using std::endl;

  vector<int> ratings(NUM);
  vector<string> titles(NUM);
  cout << "You will do exactly as told. You will enter\n"
    << NUM << " book titles and your ratings (0-10).\n";
  int i;
  for (i = 0; i < NUM; i++)
  {
    cout << "Enter title #" << i + 1 << ": ";
    getline(cin,titles[i]);
    cout << "Enter your rating (0-10): ";
    cin >> ratings[i];
    cin.get();
  }
  cout << "Thank you. You entered the following:\n"
    << "Rating\tBook\n";
  for (i = 0; i < NUM; i++)
  {
    cout << ratings[i] << "\t" << titles[i] << endl;
  }

  return 0;
}
```
