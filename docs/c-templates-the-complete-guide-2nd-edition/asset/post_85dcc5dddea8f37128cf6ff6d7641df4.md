
```cpp
template<typename T, typename U = int>
class S; // #1

template<>
class S<void> { // #2
public:
    void f();
};

template<> class S<char, char>; // #3

template<> class S<char, 0>; // ERROR: 0 cannot substitute U

int main()
{
    S<int>* pi; // OK: uses #1, no definition needed
    S<int> e1; // ERROR: uses #1, but no definition available
    S<void>* pv; // OK: uses #2
    S<void, int> sv; // OK: uses #2, definition available
    S<void, char> e2; // ERROR: uses #1, but no definition available
    S<char, char> e3; // ERROR: uses #3, but no definition available
}

template<>
class S<char, char> { // definition for #3
};
```

As this example also shows, declarations of full specializations (and of templates) do not necessarily have to be definitions. However, when a full specialization is declared, the generic definition is never used for the given set of template arguments. Hence, if a definition is needed but none is provided, the program is in error. For class template specialization, it is sometimes useful to “forward declare” types so that mutually dependent types can be constructed. A full specialization declaration is identical to a normal class declaration in this way (it is not a template declaration). The only differences are the syntax and the fact that the declaration must match a previous template declaration. Because it is not a template declaration, the members of a full class template specialization can be defined using the ordinary out-of-class member definition syntax (in other words, the `template<>` prefix cannot be specified):

```cpp
template<typename T>
class S;

template<> class S<char **> {
public:
    void print() const;
};

// the following definition cannot be preceded by template<>
void S<char **>::print() const
{
    std::cout << "pointer to pointer to char\n";
}
```

A more complex example may reinforce this notion:

```cpp
template<typename T>
class Outside {
public:
    template<typename U>
    class Inside {
    };
};

template<>
class Outside<void> {
    // there is no special connection between the following nested class
    // and the one defined in the generic template
    template<typename U>
    class Inside {
    private:
        static int count;
    };
};

// the following definition cannot be preceded by template<>
template<typename U>
int Outside<void>::Inside<U>::count = 1;
```

A full specialization is a replacement for the instantiation of a certain generic template, and it is not valid to have both the explicit and the generated versions of a template present in the same program. An attempt to use both in the same file is usually caught by a compiler:

```cpp
template<typename T>
class Invalid {
};

Invalid<double> x1; // causes the instantiation of Invalid<double>

template<>
class Invalid<double>; // ERROR: Invalid<double> already instantiated
```

Unfortunately, if the uses occur in different translation units, the problem may not be caught so easily. The following invalid C++ example consists of two files and compiles and links on many implementations, but it is invalid and dangerous:

```cpp
// Translation unit 1:
template<typename T>
class Danger {
public:
  enum { max = 10 };
};
char buffer[Danger<void>::max]; // uses generic value

extern void clear(char*);

int main()
{
  clear(buffer);
}

// Translation unit 2:
template<typename T>
class Danger;

template<>
class Danger<void> {
public:
  enum { max = 100 };
};

void clear(char* buf)
{
  // mismatch in array bound:
  for (int k = 0; k < Danger<void>::max; ++k) {
    buf[k] = '\0';
  }
}
```

This example is clearly contrived to keep it short, but it illustrates that care must be taken to ensure that the declaration of the specialization is visible to all the users of the generic template. In practical terms, this means that a declaration of the specialization should normally follow the declaration of the template in its header file. When the generic implementation comes from an external source (such that the corresponding header files should not be modified), this is not necessarily practical, but it may be worth creating a header including the generic template followed by declarations of the specializations to avoid these hard-to-find errors. We find that, in general, it is better to avoid specializing templates coming from an external source unless it is clearly marked as being designed for that purpose.

## 16.3.2 Full Function Template Specialization

The syntax and principles behind (explicit) full function template specialization are much the same as those for full class template specialization, but overloading and argument deduction come into play.

The full specialization declaration can omit explicit template arguments when the template being specialized can be determined via argument deduction (using as argument types the parameter types provided in the declaration) and partial ordering. For example:

```cpp
template<typename T>
int f(T) // #1
{
  return 1;
}

template<typename T>
int f(T*) // #2
{
  return 2;
}

template<> int f(int) // OK: specialization of #1
{
  return 3;
}

template<> int f(int*) // OK: specialization of #2
{
  return 4;
}
```

A full function template specialization cannot include default argument values. However, any default arguments that were specified for the template being specialized remain applicable to the explicit specialization:

```cpp
template<typename T>
int f(T, T x = 42)
{
  return x;
}

template<> int f(int, int = 35) // ERROR
{
  return 0;
}
```

(That’s because a full specialization provides an alternative definition, but not an alternative declaration. At the point of a call to a function template, the call is entirely resolved based on the function template.)

A full specialization is in many ways similar to a normal declaration (or rather, a normal redeclaration). In particular, it does not declare a template, and therefore only one definition of a noninline full function template specialization should appear in a program. However, we must still ensure that a declaration of the full specialization follows the template to prevent attempts at using the function generated from the template. The declarations for a template `g()` and one full specialization would therefore typically be organized in two files as follows:

- The interface file contains the definitions of primary templates and partial specializations but declares only the full specializations:

  ```cpp
  #ifndef TEMPLATE_G_HPP
  #define TEMPLATE_G_HPP

  // template definition should appear in header file:
  template<typename T>
  int g(T, T x = 42)
  {
  return x;
  }

  // specialization declaration inhibits instantiations of the template;
  // definition should not appear here to avoid multiple definition errors
  template<> int g(int, int y);

  #endif // TEMPLATE_G_HPP
  ```

- The corresponding implementation file defines the full specialization:

  ```cpp
  #include "template_g.hpp"

  template<> int g(int, int y)
  {
  return y/2;
  }
  ```

Alternatively, the specialization could be made inline, in which case its definition can be (and should be) placed in the header file.

## 16.3.3 Full Variable Template Specialization

Variable templates can also be fully specialized. By now, the syntax should be intuitive:

```cpp
template<typename T> constexpr std::size_t SZ = sizeof(T);
template<> constexpr std::size_t SZ<void> = 0;
```

Clearly, the specialization can provide an initializer that is distinct from that resulting from the template. Interestingly, a variable template specialization is not required to have a type matching that of the template being specialized:

```cpp
template<typename T> typename T::iterator null_iterator;
template<> BitIterator null_iterator<std::bitset<100>>;
// BitIterator doesn’t match T::iterator, and that is fine
```

## 16.3.4 Full Member Specialization

Not only member templates, but also ordinary static data members and member functions of class templates, can be fully specialized. The syntax requires `template<>` prefix for every enclosing class template. If a member template is being specialized, a `template<>` must also be added to denote that it is being specialized. To illustrate the implications of this, let’s assume the following declarations:

```cpp
template<typename T>
class Outer { // #1
public:
  template<typename U>
  class Inner { // #2
  private:
    static int count; // #3
  };
  static int code; // #4
  void print() const { // #5
    std::cout << "generic";
  }
};
template<typename T>
int Outer<T>::code = 6; // #6

template<typename T> template<typename U>
int Outer<T>::Inner<U>::count = 7; // #7

template<>
class Outer<bool> { // #8
public:
  template<typename U>
  class Inner { // #9
  private:
```
