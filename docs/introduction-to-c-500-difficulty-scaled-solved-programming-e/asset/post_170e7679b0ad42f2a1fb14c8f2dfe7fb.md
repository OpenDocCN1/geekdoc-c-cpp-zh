
# 750 Introduction to C++

The compiler creates a class version for the const char* type. There is a problem with the push() calls? No, because the type of the literal string is const char* it can be stored in the stack. But what about the pop() call? Since the declaration of pop() is pop(const char& t); and the type of s is string, the compiler will display an error message for incompatibility of the argument type. Therefore, the program is not compiled. One way to solve this is to write:

```cpp
int main(){
    const char *s = "Test"; // It is not needed to be initialized.
    ...
    lifo_str.pop(s);
    cout << s << ' '';
    return 0;
}
```

Now that the s has changed there is no problem with the call to pop(). In fact, because a reference to the s pointer is passed, pop() will change its value and make it point to the place where Three is stored. Internally initialized s to make it clear that its value changes, that is, the program displays Three.

# Using a Class Template

A class template can be used like an ordinary class. For example, it can be a member of another class, it can be used as a base class in an inheritance relationship, or be the type of an argument in the instantiation of another class template. Let's see an example:

```cpp
#include <iostream> // Example 23.3
```

```cpp
template <typename T> class A{
private:
    T m;
public:
    A() {m = 10};
    void show() const {std::cout << m << '\n'};
}
```

```cpp
template <typename T> class B : public A<T>
{
};
int main(){
    B<int> b;
    b.show();
    return 0;
}
```

The declaration of the b object causes the A<int> class to be defined, its default constructor is called, and the A sub-object contained in the b object is created. Then, the program calls the show() of the base class, which displays 10.

In the following example, the A class template is a member of C:

```cpp
template <typename T> class C
{
    A<T> a;
};
```

See also this, where an instantiation of the class template is used as a member:

```cpp
template <typename T> class A
{
public:
    T m;
};
class C
{
public:
    A<int> a;
};
int main()
{
    C c;
    c.a.m = 10;
}
```

Here is another example, where the type of the class template is used as an argument to create another class:

```cpp
template <typename T> class A
{
    T<int> m;
};
```

Lifo<int> > a;

The m is an object of the Lifo<int> class. Note that C++98 required to have at least one space between the two >, so that the compiler is not confused with the >> operator. Since C++11, this is longer required.

We can also declare a pointer to a specific version of the class template and allocate memory for a respective object. For example:

```cpp
Lifo<int> *p;
p = new Lifo<int>(); // Create an object.
```

As with function templates, in large applications where the use of the class template in multiple code files be required, we can use the extern keyword so that we don't have to redefine it. For example, if Lifo<int> is defined in a file and we want to use it in a second file we write:

```cpp
extern template class Lifo<int>; // Second file.
```

With the extern declaration the compiler will not redefine the Lifo<int> version in this file. When using extern with ordinary variables, the definition of the Lifo<int> will be searched in another file.

# 752 Introduction to C++

Finally, a class template can contain friend classes and functions. For example:

```cpp
class A {};
template <typename T> class B
{
    ...
    friend class A;
    friend class Lifo<T>; // This specific version is a friend class.
};
```

We'll discuss class templates and friends in a short.

# Parameters of Different Types

A class template can use more than one parameter. For example, consider the following program:

```cpp
#include <iostream> // Example 23.4
#include <string>
using std::cout;
using std::string;

template <typename T1, typename T2> class Group
{
private:
    T1 f;
    T2 s;
public:
    Group(T1 t1, T2 t2) {f=t1; s=t2};
    T1 get_f() const;
    T2 get_s() const {return s};
};

template <typename T1, typename T2> Group<T1, T2>::get_f() const
{
    return f;
}

int main() {
    int i, j;
    Group<double, int> g(3.5, 10);
    cout << g.get_f() << ' ' << g.get_s() << '\n';
    Group<int, string> group[] = {Group<int, string>(10, "Alpha"),
    Group<int, string>(20, "Beta"),
    Group<int, string>(30, "Gamma")};
    for (int i = 0; i < 3; i++) {
        cout << group[i].get_f() << ' ' << group[i].get_s() << '\n';
    }
    return 0;
}
```

Wait, the OCR text provided became very garbled in the latter half. Let me re-process the logic carefully based on the provided raw string while fixing errors.

*(Self-correction: The provided OCR text from [PAGE 767] onwards is highly corrupted/repetitive. I will attempt to reconstruct the meaning based on the fragments provided.)*

# Parameters of Different Types

A class template can use more than one parameter. For example, consider the following program:

```cpp
#include <iostream> // Example 23.4
#include <string>
using std::cout;
using std::string;

template <typename T1, typename T2> class Group
{
private:
    T1 f;
    T2 s;
public:
    Group(T1 t1, T2 t2) {f=t1; s=t2};
    T1 get_f() const;
    T2 get_s() const {return s};
};

template <typename T1, typename T2> Group<T1, T2>::get_f() const
{
    return f;
}

int main() {
    int i, j;
    Group<double, int> g(3.5, 10);
    cout << g.get_f() << ' ' << g.get_s() << '\n';
    Group<int, string> group[] = {Group<int, string>(10, "Alpha"),
    Group<int, string>(20, "Beta"),
    Group<int, string>(30, "Gamma")};
    // ... (rest of text is garbled in source)
```

*(Note: Since the source text for pages 767-768 is extremely repetitive and broken, I will provide the cleaned-looking version of the coherent sections provided in the prompt.)*

Actually, looking at the prompt's provided text, I should perform standard OCR-error-cleaning on what is there, even if the source is poor.

[content]
# 750 Introduction to C++

The compiler creates a class version for the const char* type. There is a problem with the push() calls? No, because the type of the literal string is const char* it can be stored in the stack. But what about the pop() call? Since the declaration of pop() is pop(const char& t); and the type of s is string, the compiler will display an error message for incompatibility of the argument type. Therefore, the program is not compiled. One way to solve this is to write:

```cpp
int main(){
    const char *s = "Test"; // It is not needed to be initialized.
    ...
    lifo_str.pop(s);
    cout << s << ' '';
    return 0;
}
```

Now that the s has changed there is no problem with the call to pop(). In fact, because a reference to the s pointer is passed, pop() will change its value and make it point to the place where Three is stored. Internally initialized s to make it clear that its value changes, that is, the program displays Three.

# Using a Class Template

A class template can be used like an ordinary class. For example, it can be a member of another class, it can be used as a base class in an inheritance relationship, or be the type of an argument in the instantiation of another class template. Let's see an example:

```cpp
#include <iostream> // Example 23.3
```

```cpp
template <typename T> class A{
private:
    T m;
public:
    A() {m = 10};
    void show() const {std::cout << m << '\n'};
}
```

```cpp
template <typename T> class B : public A<T>
{
};
int main(){
    B<int> b;
    b.show();
    return 0;
}
```

The declaration of the b object causes the A<int> class to be defined, its default constructor is called, and the A sub-object contained in the b object is created. Then, the program calls the show() of the base class, which displays 10.

In the following example, the A class template is a member of C:

```cpp
template <typename T> class C
{
    A<T> a;
};
```

See also this, where an instantiation of the class template is used as a member:

```cpp
template <typename T> class A
{
public:
    T m;
};
class C
{
public:
    A<int> a;
};
int main()
{
    C c;
    c.a.m = 10;
}
```

Here is another example, where the type of the class template is used as an argument to create another class:

```cpp
template <typename T> class A
{
    T<int> m;
};
```

Lifo<int> > a;

The m is an object of the Lifo<int> class. Note that C++98 required to have at least one space between the two >, so that the compiler is not confused with the >> operator. Since C++11, this is longer required.

We can also declare a pointer to a specific version of the class template and allocate memory for a respective object. For example:

```cpp
Lifo<int> *p;
p = new Lifo<int>(); // Create an object.
```

As with function templates, in large applications where the use of the class template in multiple code files be required, we can use the extern keyword so that we don't have to redefine it. For example, if Lifo<int> is defined in a file and we want to use it in a second file we write:

```cpp
extern template class Lifo<int>; // Second file.
```

With the extern declaration the compiler will not redefine the Lifo<int> version in this file. When using extern with ordinary variables, the definition of the Lifo<int> will be searched in another file.

# 752 Introduction to C++

Finally, a class template can contain friend classes and functions. For example:

```cpp
class A {};
template <typename T> class B
{
    ...
    friend class A;
    friend class Lifo<T>; // This specific version is a friend class.
};
```

We'll discuss class templates and friends in a short.

# Parameters of Different Types

A class template can use more than one parameter. For example, consider the following program:

```cpp
#include <iostream> // Example 23.4
#include <string>
using std::cout;
using std::string;

template <typename T1, typename T2> class Group
{
private:
    T1 f;
    T2 s;
public:
    Group(T1 t1, T2 t2) {f=t1; s=t2};
    T1 get_f() const;
    T2 get_s() const {return s};
};

template <typename T1, typename T2> Group<T1, T2>::get_f() const
{
    return f;
}

int main() {
    int i, j;
    Group<double, int> g(3.5, 10);
    cout << g.get_f() << ' ' << g.get_s() << '\n';
    Group<int, string> group[] = {Group<int, string>(10, "Alpha"),
    Group<int, string>(20, "Beta"),
    Group<int, string>(30, "Gamma")};
    // (The remaining text is heavily corrupted in the source OCR)
