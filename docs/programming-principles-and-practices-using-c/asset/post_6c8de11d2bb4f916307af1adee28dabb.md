
That’s just our **vector of doubles** from §19.2.6 with **double** replaced by the template parameter **T**. We can use this class template **vector** like this:

```cpp
vector<double> vd;            // T is double
vector<int> vi;               // T is int
vector<double*> vpd;          // T is double*
vector<vector<int>> vvi;      // T is vector<T>, in which T is int
```

One way of thinking about what a compiler does when we use a template is that it generates the class with the actual type (the template argument) in place of the template parameter. For example, when the compiler sees **vector<char>** in the code, it (somewhere) generates something like this:

```cpp
class vector_char {
  int sz;                    // the size
  char* elem;               // a pointer to the elements
  int space;                // size + free space
public:
  vector_char() : sz(0), elem(nullptr), space(0) { }
  explicit vector_char(int s) :sz(s), elem(new char[s]), space(s)
  {
    for (int i=0; i<sz; ++i) elem[i]=0;    // elements are initialized
  }

  vector_char(const vector_char&);          // copy constructor
  vector_char& operator=(const vector_char&); // copy assignment

  vector_char(vector_char&&);               // move constructor
  vector_char& operator=(vector_char&&);    // move assignment

  ~vector_char ();                          // destructor

  char& operator[] (int n) { return elem[n];} // access: return reference
  const char& operator[] (int n) const { return elem[n]; }

  int size() const;                         // the current size
  int capacity() const;

  void resize(int newsize);                  // growth
  void push_back(const char& d);
  void reserve(int newalloc);
};
```

For **vector<double>**, the compiler generates roughly the **vector** (of **double**) from §19.2.6 (using a suitable internal name meaning **vector<double>**).

Sometimes, we call a class template a *type generator*. The process of generating types (classes) from a class template given template arguments is called *specialization* or *template instantiation*. For example, **vector<char>** and **vector<Poly_line>** are said to be specializations of **vector**. In simple cases, such as our **vector**, instantiation is a pretty simple process. In the most general and advanced cases, template instantiation is horrendously complicated. Fortunately for the user of templates, that complexity is in the domain of the compiler writer, not the template user. Template instantiation (generation of template specializations) takes place at compile time or link time, not at run time.

Naturally, we can use member functions of such a class template. For example:

```cpp
void fct(vector<string>& v)
{
    int n = v.size();
    v.push_back("Norah");
    // ...
}
```

When such a member function of a class template is used, the compiler generates the appropriate function. For example, when the compiler sees **v.push_back("Norah")**, it generates a function

```cpp
void vector<string>::push_back(const string& d) {/*...*/}
```

from the template definition

```cpp
template<typename T> void vector<T>::push_back(const T& d) {/*...*/};
```

That way, there is a function for **v.push_back("Norah")** to call. In other words, when you need a function for given object and argument types, the compiler will write it for you based on its template.

Instead of writing **template<typename T>**, you can write **template<class T>**. The two constructs mean exactly the same thing, but some prefer *typename* “because it is clearer” and “because nobody gets confused by *typename* thinking that you can’t use a built-in type, such as **int**, as a template argument.” We are of the opinion that **class** already means type, so it makes no difference. Also, **class** is shorter.

### 19.3.2 Generic programming

Templates are the basis for generic programming in C++. In fact, the simplest definition of “generic programming” in C++ is “using templates.” That definition is a bit too simple-minded, though. We should not define fundamental programming concepts in terms of programming language features. Programming language features exist to support programming techniques – not the other way around. As with most popular notions, there are many definitions of “generic programming.” We think that the most useful simple definition is

*Generic programming*: Writing code that works with a variety of types presented as arguments, as long as those argument types meet specific syntactic and semantic requirements.

For example, the elements of a **vector** must be of a type that we can copy (by copy construction and copy assignment), and in Chapters 20 and 21 we will see templates that require arithmetic operations on their arguments. When *what* we parameterize is a class, we get a *class template*, what is often called a *parameterized type* or a *parameterized class*. When *what* we parameterize is a function, we get a *function template*, what is often called a *parameterized function* and sometimes also called an *algorithm*. Thus, generic programming is sometimes referred to as “algorithm-oriented programming”; the focus of the design is more the algorithms than the data types they use.

Since the notion of parameterized types is so central to programming, let's explore the somewhat bewildering terminology a bit further. That way we have a chance of not getting too confused when we meet such notions in other contexts.

This form of generic programming relying on explicit template parameters is often called *parametric polymorphism*. In contrast, the polymorphism you get from using class hierarchies and virtual functions is called *ad hoc polymorphism* and that style of programming is called *object-oriented programming* (§14.3–4). The reason that both styles of programming are called *polymorphic* is that each style relies on the programmer to present many versions of a concept by a single interface. *Polymorphism* is Greek for “many shapes,” referring to the many different types you can manipulate through a common interface. In the **Shape** example from Chapters 16–19 we literally accessed many shapes (such as **Text**, **Circle**, and **Polygon**) through the interface defined by **Shape**. When we use **vectors**, we use many **vectors** (such as **vector<int>**, **vector<double>**, and **vector<Shape>**) through the interface defined by the **vector** template.

There are several differences between object-oriented programming (using class hierarchies and virtual functions) and generic programming (using templates). The most obvious is that the choice of function invoked when you use generic programming is determined by the compiler at compile time, whereas for object-oriented programming, it is not determined until run time. For example:

```cpp
v.push_back(x);       // put x into the vector v
s.draw();             // draw the shape s
```

For `v.push_back(x)` the compiler will determine the element type for **v** and use the appropriate `push_back()`, but for `s.draw()` the compiler will indirectly call some `draw()` function (using **s**'s *vtbl*; see §14.3.1). This gives object-oriented programming a degree of freedom that generic programming lacks, but leaves run-of-the-mill generic programming more regular, easier to understand, and better performing (hence the “ad hoc” and “parametric” labels).

To sum up:

- *Generic programming:* supported by templates, relying on compile-time resolution
- *Object-oriented programming:* supported by class hierarchies and virtual functions, relying on run-time resolution

Combinations of the two are possible and useful. For example:

```cpp
void draw_all(vector<Shape*>& v)
{
    for (int i = 0; i<v.size(); ++i) v[i]->draw();
}
```

Here we call a virtual function (`draw()`) on a base class (`Shape`) using a virtual function – that’s certainly object-oriented programming. However, we also kept `Shape*`s in a `vector`, which is a parameterized type, so we also used (simple) generic programming.

So – assuming you have had your fill of philosophy for now – what do people actually use templates for? For unsurpassed flexibility and performance:

- Use templates where performance is essential (e.g., numerics and hard real time; see Chapters 24 and 25).
- Use templates where flexibility in combining information from several types is essential (e.g., the C++ standard library; see Chapters 20–21).

### 19.3.3 Concepts

Templates have many useful properties, such as great flexibility and near-optimal performance, but unfortunately they are not perfect. As usual, the benefits have corresponding weaknesses. For templates, the main problem is that the flexibility and performance come at the cost of poor separation between the “inside” of a template (its definition) and its interface (its declaration). This manifests itself in poor error diagnostics – often spectacularly poor error messages. Sometimes, these error messages come much later in the compilation process than we would prefer.
