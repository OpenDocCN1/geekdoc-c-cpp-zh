
## Part II
## Templates in Depth

The first part of this book provided a tutorial for most of the language concepts underlying C++ templates. That presentation is sufficient to answer most questions that may arise in everyday C++ programming. The second part of this book provides a reference that answers even the more unusual questions that arise when pushing the envelope of the language to achieve some advanced software effects. If desired, you can skip this part on a first read and return to specific topics as prompted by references in later chapters or after looking up a concept in the index.

Our goal is to be clear and complete but also to keep the discussion concise. To this end, our examples are short and often somewhat artificial. This also ensures that we don’t stray from the topic at hand to unrelated issues.

In addition, we look at possible future changes and extensions for the templates language feature in C++.

The topics of this part include:
- Fundamental template declaration issues
- The meaning of names in templates
- The C++ template instantiation mechanisms
- The template argument deduction rules
- Specialization and overloading
- Future possibilities

## Chapter 12
## Fundamentals in Depth

In this chapter we review some of the fundamentals introduced in the first part of this book *in depth*: the declaration of templates, the restrictions on template parameters, the constraints on template arguments, and so forth.

### 12.1 Parameterized Declarations

C++ currently supports four fundamental kinds of templates: class templates, function templates, variable templates, and alias templates. Each of these template kinds can appear in namespace scope, but also in class scope. In class scope they become nested class templates, member function templates, static data member templates, and member alias templates. Such templates are declared much like ordinary classes, functions, variables, and type aliases (or their class member counterparts) except for being introduced by a *parameterization clause* of the form `template<parameters here>` Note that C++17 introduced another construct that is introduced with such a parameterization clause: *deduction guides* (see Section 2.9 on page 42 and Section 15.12.1 on page 314). Those aren’t called *templates* in this book (e.g., they are not instantiated), but the syntax was chosen to be reminiscent of function templates.

We’ll come back to the actual template parameter declarations in a later section. First, some examples illustrate the four kinds of templates. They can occur in *namespace scope* (globally or in a namespace) as follows: Click here to view code image

*details/definitions1.hpp*

```
template<typename T> // a namespace scope class template
class Data {
public:
static constexpr bool copyable = true;
...;
};
```

```
template<typename T> // a namespace scope function template
void log (T x) {
...
}

template<typename T> // a namespace scope variable template (since C++14)
T zero = 0;

template<typename T> // a namespace scope variable template (since C++14)
bool dataCopyable = Data<T>::copyable;

template<typename T> // a namespace scope alias template
using DataList = Data<T*>;
```

Note that in this example, the static data member Data<T>::copyable is not a variable template, even though it is indirectly parameterized through the parameterization of the class template Data. However, a variable template can appear in class scope (as the next example will illustrate), and in that case it is a static data member template.

The following example shows the four kinds of templates as class members that are defined within their parent class: Click here to view code image

# details/definitions2.hpp

```
class Collection {
public:
template<typename T> // an in-class member class template definition
class Node {
... 
};

template<typename T> // an in-class (and therefore implicitly inline)
T* alloc() { //member function template definition
...
}

template<typename T> // a member variable template (since C++14)
static T zero = 0;
template<typename T> // a member alias template
using NodePtr = Node<T>*;
};
```

Note that in C++17, variables—including static data members—and variable templates can be “in-line,” which means that their definition can be repeated across translation units. This is redundant for variable templates, which can always be defined in multiple translation units. Unlike member functions, however, a static data member being defined in its enclosing class does not make it inline: The keyword inline must be specified in all cases.

Finally, the following code demonstrates how member templates that are not alias templates can be defined out-of-class: Click here to view code image

# details/definitions3.hpp

```
template<typename T> // a namespace scope class template
class List {
public:
List() = default; // because a template constructor is defined

template<typename U> // another member class template,
class Handle; // without its definition

template<typename U> // a member function template
List (List<U> const&); // (constructor)

template<typename U> // a member variable template (since C++14)
static U zero;
};

template<typename T> // out-of-class member class template definition
template<typename U>
class List<T>::Handle {
...
};

template<typename T> // out-of-class member function template
definition
template<typename T2>
List<T>::List (List<T2> const& b)
{
...
}

template<typename T> // out-of-class static data member template
definition
template<typename U>
U List<T>::zero = 0;
```

Member templates defined outside their enclosing class may need multiple template<...> parameterization clauses: one for every enclosing class template and one for the member template itself. The clauses are listed starting from the outermost class template.

Note also that a constructor template (a special kind of member function template) disables the implicit declaration of the default constructor (because it is only implicitly declared if no other constructor is declared). Adding a defaulted declaration List() = default; ensures an instance of List<T> is default-constructible with the semantics of an implicitly declared constructor.

### Union Templates

Union templates are possible too (and they are considered a kind of class template): Click here to view code image

```
template<typename T>
union AllocChunk {
T object;
unsigned char bytes[sizeof(T)];
};
```

### Default Call Arguments

Function templates can have default call arguments just like ordinary function declarations: Click here to view code image

```
template<typename T>
void report_top (Stack<T> const&, int number = 10);
```

```
template<typename T>
void fill (Array<T>&, T const& = T{}); // T{} is zero for built-in types
```

The latter declaration shows that a default call argument could depend on a template parameter. It also can be defined as (the only way possible before C++11, see Section 5.2 on page 68) Click here to view code image

```
template<typename T>
void fill (Array<T>&, T const& = T()); // T() is zero for built-in types
```

When the fill() function is called, the default argument is not instantiated if a second function call argument is supplied. This ensures that no error is issued if the default call argument cannot be instantiated for a particular T. For example: Click here to view code image

```
class Value {
public:
explicit Value(int); // no default constructor
};

void init (Array<Value>& array)
{
Value zero(0);

fill(array, zero); // OK: default constructor not used
fill(array); // ERROR: undefined default constructor for Value is used
}
```

### Nontemplate Members of Class Templates

In addition to the four fundamental kinds of templates declared inside a class, you can also have ordinary class members parameterized by being part of a class template They are occasionally (erroneously) also referred to as member templates. Although they can be parameterized, such definitions aren’t quite first-class templates. Their parameters are entirely determined by the template of which they are members. For example: Click here to view code image

```
template<int I>
class CupBoard
{
class Shelf; // ordinary class in class template
void open(); // ordinary function in class template
enum Wood : unsigned char; // ordinary enumeration type in class template
static double totalWeight; // ordinary static data member in class template
};
```

The corresponding definitions only specify a parameterization clause for the parent class templates, but not for the member itself, because it is not a template (i.e., no parameterization clause is associated with the name appearing after the last ::): Click here to view code image

```
template<int I> // definition of ordinary class in class template
class CupBoard<I>::Shelf {
...
};

template<int I> // definition of ordinary function in class template
void CupBoard<I>::open()
{
...
}

template<int I> // definition of ordinary enumeration type class in class template
enum CupBoard<I>::Wood {
Maple, Cherry, Oak
};

template<int I> // definition of ordinary static member in class template
double CupBoard<I>::totalWeight = 0.0; Since C++17, the static
