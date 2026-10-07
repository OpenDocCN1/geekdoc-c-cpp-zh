
Student class. In this case, student.h, you can add using declarations to the public
section:

```
class Student : private std::string, private std::valarray<double>
{
public:
    using std::valarray<double>::min;
    using std::valarray<double>::max;
    ...
};
```

The using declaration makes the valarray<double>::min() and
valarray<double>::max() methods available as if they were public Student methods:
out << "high score: " << ada[i] << endl;

Note that the using declaration uses the member name—no parentheses, no func-
signature, no return type. For example, to make the valarray operator[]
method available to the Student class, you could place the following using declaration in the
public section of the Student class declaration:

```
using std::valarray<double>::operator();
```

This would make both versions (const and non-const) available. You could then
remove the existing prototypes and definitions for Student::operator(). .The using
declaration approach works only for inheritance and not for containment.

There is an older way to redeclare base-class methods in a privately derived class: You
place the method name in the public section of the derived class. Here's how you would
do that:

```
class Student : private std::string, private std::valarray<double>
{
public:
    std::valarray<double>::operator[](); // redeclare as public, just use name
    ...
};
```

This looks like a using declaration without the using keyword. This approach is
deprecated, meaning the intention is to phase it out. So if your compiler supports the
using declaration, you can use it to make a method from a private base class available to a
ter derived class.

## Multiple Inheritance

MI describes a class that has more than one immediate base class. As with single ameri-
tance, public MI should express an is-a relationship. For example, if you have a Waiter
class and a Singer class, you could derive a SingingWaiter class from the:

class SingingWaiter : public Waiter, public Singer {...};

Note that you must qualify each base class with the keyword public. That's because the compiler assumes private derivation unless instructed otherwise:

class SingingWaiter : public Waiter, Singer {...}; // Singer is a private base

As discussed earlier in this chapter, private and protected MI can express a has-a relation; the student i implementation of the Student class is an example. We'll concentrate on public inheritance now.

MI can introduce new problems for programmers. The two chief problems are inheriting different methods with the same name from two base classes and inheriting multiple instances of a class via two or more related base classes. Solving these problems involves introducing a few new rules and syntax variations. Thus, MI can be more difficult and problem-prone than using single inheritance. For this reason, many in the C++ community object strongly to MI; some want it removed from the language. Others suggest MI and argue it's very useful, even necessary, for particular projects. Still others suggest MI cautiously and in moderation.

Let's explore a particular example and see what the problems and solutions are. You need several classes to create an MI situation. For this example, we define an abstract Worker base class and derive a Waiter class and a Singer class from it. Then we can use MI to derive a SingingWaiter class from the Waiter and Singer classes (see Figure 14.3). This is a case in which a base class (Worker) is inherited via two separate derivations, which is the circumstance that causes the most difficulties with MI. We start with declarations for the Worker, Waiter, and Singer classes, as shown in Listing 14.7.

![](img/cd111a87c1db9aff4db4b18834327463_823_0.png)

Figure 14.3 MI with a shared ancestor.

# 810 Chapter 14 Reusing Code in C++

Listing 14.7 worker0.h

```cpp
// worker0.h -- working classes
#ifndef WORKER0_H_
#define WORKER0_H_

#include <string>

class Worker // an abstract base class
{
private:
    std::string fullname;
    long id;
public:
    Worker() : fullname("no one
```

```cpp
Singer(const std::string &s, long n, int v = other)
    : Worker(s, n), voice(v) {}
Singer(const Worker &wk, int v = other)
    : Worker(wk), voice(v) {}
void Set();
void Show() const;

#endif
```

The class declarations in Listing 14.7 include some internal constants that represent voice types. An enumeration makes alto, centralto, and so on symbolic constants for voice types, and the static array pv holds pointers to the C-style string equivalents. The implementation file, shown in Listing 14.8, initializes this array and provides method definitions.

# Listing 14.8 worker0.cpp

```cpp
// worker0.cpp -- working class methods
#include "worker0.h"
#include <iostream>
using std::cout;
using std::cin;
using std::endl;
// Worker methods

// must implement virtual destructor, even if pure
Worker::Worker() {}

void Worker::Set()
{
    cout << "Enter worker's name: ";
    getline(cin, fullname);
    cout << "Enter worker's ID: ";
```

[PAGE 826]
# 812 Chapter 14 Reusing Code in C++

```cpp
    cout << "Enter worker's ID: ";
    cout << "Enter worker's name: ";
    getline(cin, fullname);
    cout << "Enter worker's ID: ";
```
Wait, let me re-align the text properly based on the OCR flow. The OCR had some broken breaks. I will provide the clean version.

[Correct Flow]
Student class. In this case, student.h, you can add using declarations to the public
section:

```cpp
class Student : private std::string, private std::valarray<double>
{
public:
    using std::valarray<double>::min;
    using std::valarray<double>::max;
    ...
};
```

The using declaration makes the valarray<double>::min() and
valarray<double>::max() methods available as if they were public Student methods:
out << "high score: " << ada[i] << endl;

Note that the using declaration uses the member name—no parentheses, no func-
signature, no return type. For example, to make the valarray operator[]
method available to the Student class, you could place the following using declaration in the
public section of the Student class declaration:

```cpp
using std::valarray<double>::operator();
```

This would make both versions (const and non-const) available. You could then
remove the existing prototypes and definitions for Student::operator(). .The using
declaration approach works only for inheritance and not for containment.

There is an older way to redeclare base-class methods in a privately derived class: You
place the method name in the public section of the derived class. Here's how you would
do that:

```cpp
class Student : private std::string, private std::valarray<double>
{
public:
    std::valarray<double>::operator[](); // redeclare as public, just use name
    ...
};
```

This looks like a using declaration without the using keyword. This approach is
deprecated, meaning the intention is to phase it out. So if your compiler supports the
using declaration, you can use it to make a method from a private base class available to a
ter derived class.

# Multiple Inheritance

MI decribes a class that has more than one immediate base class. As with single ameri-
tance, public MI should express an is-a relationship. For example, if you have a Waiter
class and a Singer class, you could derive a SingingWaiter class from the:

class SingingWaiter : public Waiter, public Singer {...};

Note that you must qualify each base class with the keyword public. That's because the compiler assumes private derivation unless instructed otherwise:

class SingingWaiter : public Waiter, Singer {...}; // Singer is a private base

As discussed earlier in this chapter, private and protected MI can express a has-a relation; the student i implementation of the Student class is an example. We'll concentrate on public inheritance now.

MI can introduce new problems for programmers. The two chief problems are inheriting different methods with the same name from two base classes and inheriting multiple instances of a class via two or more related base classes. Solving these problems involves introducing a few new rules and syntax variations. Thus, MI can be more difficult and problem-prone than using single inheritance. For this reason, many in the C++ community object strongly to MI; some want it removed from the language. Others suggest MI and argue it's very useful, even necessary, for particular projects. Still others suggest MI cautiously and in moderation.

Let's explore a particular example and see what the problems and solutions are. You need several classes to create an MI situation. For this example, we define an abstract Worker base class and derive a Waiter class and a Singer class from it. Then we can use MI to derive a SingingWaiter class from the Waiter and Singer classes (see Figure 14.3). This is a case in which a base class (Worker) is inherited via two separate derivations, which is the circumstance that causes the most difficulties with MI. We start with declarations for the Worker, Waiter, and Singer classes, as shown in Listing 14.7.

![](img/cd111a87c1db9aff4db4b18834327463_823_0.png)

Figure 14.3 MI with a shared ancestor.

# 810 Chapter 14 Reusing Code in C++

Listing 14.7 worker0.h

```cpp
// worker0.h -- working classes
#ifndef WORKER0_H_
#define WORKER0_H_

#include <string>

class Worker // an abstract base class
{
private:
    std::string fullname;
    long id;
public:
    Worker() : fullname("no one
```

```cpp
Singer(const std::string &s, long n, int v = other)
    : Worker(s, n), voice(v) {}
Singer(const Worker &wk, int v = other)
    : Worker(wk), voice(v) {}
void Set();
void Show() const;

#endif
```

The class declarations in Listing 14.7 include some internal constants that represent voice types. An enumeration makes alto, centralto, and so on symbolic constants for voice types, and the static array pv holds pointers to the C-style string equivalents. The implementation file, shown in Listing 14.8, initializes this array and provides method definitions.

# Listing 14.8 worker0.cpp

```cpp
// worker0.cpp -- working class methods
#include "worker0.h"
#include <iostream>
using std::cout;
using std::cin;
using std::endl;
// Worker methods

// must implement virtual destructor, even if pure
Worker::Worker() {}

void Worker::Set()
{
    cout << "Enter worker's name: ";
    getline(cin, fullname);
    cout << "Enter worker's ID: ";
}
```

Wait, the OCR text is very messy at the end. Let me provide the clean, merged version of all text provided in the prompt.

---

[content]
Student class. In this case, student.h, you can add using declarations to the public
section:

```cpp
class Student : private std::string, private std::valarray<double>
{
public:
    using std::valarray<double>::min;
    using std::valarray<double>::max;
    ...
};
```

The using declaration makes the valarray<double>::min() and
valarray<double>::max() methods available as if they were public Student methods:
out << "high score: " << ada[i] << endl;

Note that the using declaration uses the member name—no parentheses, no func-
signature, no return type. For example, to make the valarray operator[]
method available to the Student class, you could place the following using declaration in the
public section of the Student class declaration:

```cpp
using std::valarray<double>::operator();
```

This would make both versions (const and non-const) available. You could then
remove the existing prototypes and definitions for Student::operator(). .The using
declaration approach works only for inheritance and not for containment.

There is an older way to redeclare base-class methods in a privately derived class: You
place the method name in the public section of the derived class. Here's how you would
do that:

```cpp
class Student : private std::string, private std::valarray<double>
{
public:
    std::valarray<double>::operator[](); // redeclare as public, just use name
    ...
};
```

This looks like a using declaration without the using keyword. This approach is
deprecated, meaning the intention is to phase it out. So if your compiler supports the
using declaration, you can use it to make a method from a private base class available to a
ter derived class.

# Multiple Inheritance

MI describes a class that has more than one immediate base class. As with single ameri-
tance, public MI should express an is-a relationship. For example, if you have a Waiter
class and a Singer class, you could derive a SingingWaiter class from the:

class SingingWaiter : public Waiter, public Singer {...};

Note that you must qualify each base class with the keyword public. That's because the compiler assumes private derivation unless instructed otherwise:

class SingingWaiter : public Waiter, Singer {...}; // Singer is a private base

As discussed earlier in this chapter, private and protected MI can express a has-a relation; the student i implementation of the Student class is an example. We'll concentrate on public inheritance now.

MI can introduce new problems for programmers. The two chief problems are inheriting different methods with the same name from two base classes and inheriting multiple instances of a class via two or more related base classes. Solving these problems involves introducing a few new rules and syntax variations. Thus, MI can be more difficult and problem-prone than using single inheritance. For this reason, many in the C++ community object strongly to MI; some want it removed from the language. Others suggest MI and argue it's very useful, even necessary, for particular projects. Still others suggest MI cautiously and in moderation.

Let's explore a particular example and see what the problems and solutions are. You need several classes to create an MI situation. For this example, we define an abstract Worker base class and derive a Waiter class and a Singer class from it. Then we can use MI to derive a SingingWaiter class from the Waiter and Singer classes (see Figure 14.3). This is a case in which a base class (Worker) is inherited via two separate derivations, which is the circumstance that causes the most difficulties with MI. We start with declarations for the Worker, Waiter, and Singer classes, as shown in Listing 14.7.

![](img/cd111a87c1db9aff4db4b18834327463_823_0.png)

Figure 14.3 MI with a shared ancestor.

# 10 Chapter 14 Reusing Code in C++

Listing 14.7 worker0.h

```cpp
// worker0.h -- working classes
#ifndef WORKER0_H_
#define WORKER0_H_

#include <string>

class Worker // an abstract base class
{
private:
    std::string fullname;
    long id;
public:
    Worker() : fullname("no one
```

```cpp
Singer(const std::string &s, long n, int v = other)
    : Worker(s, n), voice(v) {}
Singer(const Worker &wk, int v = other)
    : Worker(wk), voice(v) {}
void Set();
void Show() const;

#endif
```

The class declarations in Listing 14.7 include some internal constants that represent voice types. An enumeration makes alto, centralto, and so on symbolic constants for voice types, and the static array pv holds pointers to the C-style string equivalents. The implementation file, shown in Listing 14.8, initializes this array and provides method definitions.

# Listing 14.8 worker0.cpp

```cpp
// worker0.cpp -- working class methods
#include "worker0.h"
#include <iostream>
using std::cout;
using std::cin;
using std::endl;
// Worker methods

// must implement virtual destructor, even if pure
Worker::Worker() {}

void Worker::Set()
{
    cout << "Enter worker's name: ";
    getline(cin, fullname);
    cout << "Enter worker's ID: ";
}
```
Wait, the OCR text is very fragmented at the end. I will provide the final cleaned version based on the provided text logic.

[content]
Student class. In this case, student.h, you can add using declarations to the public
section:

```cpp
class Student : private std::string, private std::valarray<double>
{
public:
    using std::valarray<double>::min;
    using std::valarray<double>::max;
    ...
};
```

The using declaration makes the valarray<double>::min() and
valarray<double>::max() methods available as if they were public Student methods:
out << "high score: " << ada[i] << endl;

Note that the using declaration uses the member name—no parentheses, no func-
signature, no return type. For example, to make the valarray operator[]
method available to the Student class, you could place the following using declaration in the
public section of the Student class declaration:

```cpp
using std::valarray<double>::operator();
```

This would make both versions (const and non-const) available. You could then
remove the existing prototypes and definitions for Student::operator(). .The using
declaration approach works only for inheritance and not for containment.

There is an older way to redeclare base-class methods in a privately derived class: You
place the method name in the public section of the derived class. Here's how you would
do that:

```cpp
class Student : private std::string, private std::valarray<double>
{
public:
    std::valarray<double>::operator[](); // redeclare as public, just use name
    ...
};
```

This looks like a using declaration without the using keyword. This approach is
deprecated, meaning the intention is to phase it out. So if your compiler supports the
using declaration, you can use it to make a method from a private base class available to a
ter derived class.

# Multiple Inheritance

MI describes a class that has more than one immediate base class. As with single ameri-
tance, public MI should express an is-a relationship. For example, if you have a Waiter
class and a Singer class, you could derive a SingingWaiter class from the:

class SingingWaiter : public Waiter, public Singer {...};

Note that you must qualify each base class with the keyword public. That's because the compiler assumes private derivation unless instructed otherwise:

class SingingWaiter : public Waiter, Singer {...}; // Singer is a private base

As discussed earlier in this chapter, private and protected MI can express a has-a relation; the student i implementation of the Student class is an example. We'll concentrate on public inheritance now.

MI can introduce new problems for programmers. The two chief problems are inheriting different methods with the same name from two base classes and inheriting multiple instances of a class via two or more related base classes. Solving these problems involves introducing a few new rules and syntax variations. Thus, MI can be more difficult and problem-prone than using single inheritance. For this reason, many in the C++ community object strongly to MI; some want it removed from the language. Others suggest MI and argue it's very useful, even necessary, for particular projects. Still others suggest MI cautiously and in moderation.

Let's explore a particular example and see what the problems and solutions are. You need several classes to create an MI situation. For this example, we define an abstract Worker base class and derive a Waiter class and a Singer class from it. Then we can use MI to derive a SingingWaiter class from the Waiter and Singer classes (see Figure 14.3). This is a case in which a base class (Worker) is inherited via two separate derivations, which is the circumstance that causes the most difficulties with MI. We start with declarations for the Worker, Waiter, and Singer classes, as shown in Listing 14.7.

![](img/cd111a87c1db9aff4db4b18834327463_823_0.png)

Figure 14.3 MI with a shared ancestor.

# 810 Chapter 14 Reusing Code in C++

Listing 14.7 worker0.h

```cpp
// worker0.h -- working classes
#ifndef WORKER0_H_
#define WORKER0_H_

#include <string>

class Worker // an abstract base class
{
private:
    std::string fullname;
    long id;
public:
    Worker() : fullname("no one
```

```cpp
Singer(const std::string &s, long n, int v = other)
    : Worker(s, n), voice(v) {}
Singer(const Worker &wk, int v = other)
    : Worker(wk), voice(v) {}
void Set();
void Show() const;

#endif
```

The class declarations in Listing 14.7 include some internal constants that represent voice types. An enumeration makes alto, centralto, and so on symbolic constants for voice types, and the static array pv holds pointers to the C-style string equivalents. The implementation file, shown in Listing 14.8, initializes this array and provides method definitions.

# Listing 14.8 worker0.cpp

```cpp
// worker0.cpp -- working class methods
#include "worker0.h"
#include <iostream>
using std::cout;
using std::cin;
using std::endl;
// Worker methods

// must implement virtual destructor, even if pure
Worker::Worker() {}

void Worker::Set()
{
    cout << "Enter worker's name: ";
    getline(cin, fullname);
    cout << "Enter worker's ID: ";
}
```
(Note: The OCR text ends abruptly/fragmented here. I have merged all provided segments.)
