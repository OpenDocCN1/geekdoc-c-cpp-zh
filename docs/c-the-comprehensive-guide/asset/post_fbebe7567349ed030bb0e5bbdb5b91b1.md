
```cpp
int main() {
    cout << length("Hipphopp") << "\n";  // const char* to string
    cout << twice(10).value_ << "\n";      // int to Value
    string name {"Gandalf"};
    cout << ( name + " the Grey") << "\n"; // string + const char*
}
```

**Listing 16.2** When you call a function with a parameter for which the compiler invokes a constructor to perform a conversion, it creates a temp-value.

The length function takes a string as an argument. However, when I call length("Hipphopp"), I am passing a text literal, which is a `const char[]`. The compiler automatically creates a string just for the purpose of passing it to length(). After the statement, this created string disappears because it is a temp-value.

The mechanism the compiler uses is already known to you: automatic type conversion. The same thing happens with twice(10). Because Value has a constructor with one argument, the compiler can use it for automatic type conversion. And lo and behold, 10 is an int and fits—so a temporary Value is created, used within twice as v, and discarded at the end.

Especially binary operators like to create temporary values, such as plus +. The name+" the Grey" expression is the call of the operator+ with the string and const char* argument types. The operator concatenates the arguments into a new string, which is then output. The concatenated result is the temp-value and is no longer needed after the ;.

### Background: Lvalues, Rvalues, and Legal Theft

In the context of temp-values, you will often encounter terms like *lvalue*, *rvalue*, and *rvalue references* in reference books and on the internet. These are not features that C++ brings, but rather the technical terms used to describe how C++ implements certain concepts. As a concept behind rvalue, I find the term *temp-value* better. Nevertheless, when trying to understand the how and why, you will often come across the technical terms. In the following list, assume you have declared `int x, *p, a[10]`:

- **Lvalue**  
  An expression to which you can assign something, like `x=1`, `*p=1` or `a[2]=1`. The letter *l* comes from left, because these can appear on the left side of an assignment—that is, `lvalue = ...`
- **Rvalue**  
  An expression to which you cannot assign anything, like `42=1`, `&x=1` or `x+1=1`. These are expressions that can only appear on the right side of an assignment—that is, `... = rvalue`.

> The distinction is important because an rvalue only exists briefly (if at all)—hence my term, *temp-value*. The content of temp-values can be changed without affecting any other part of the program. Typically, one transfers a resource from a temp-value to another object to save a copy. This is important for understanding move operations, which are discussed in Section 16.9.

## 16.3 The Destructor to the Constructor

If you want to check when an object is destroyed, then do it in the *destructor*. As a counterpart to the constructor, it is used to perform cleanup tasks. This can involve clearing the class's data fields or other administrative tasks.

Because you are only familiar with data structures that are automatically deinitialized, output a text as an administrative task. Fill the MyValue class from the introductory example with some life.

```cpp
// https://godbolt.org/z/WPcTv37xKM
#include <string>
#include <iostream>
#include <iomanip>    // setw
using std::cout; using std::setw; using std::string;
struct MyValue {
    static int counter;          // static: exists only once for all instances
    int number_;                  // indentation level of this instance for output
    string name_;                 // name of this instance for output
    explicit MyValue(string name)
        : number_{++counter}     // increment indentation level per instance
        , name_{name}             // remember the object's name for output
    {
        cout << setw(number_) << " " << "Constructor " << name_ << "\n"; // output instance name
    }
    ~MyValue() {                  // destructor
        cout << setw(number_) << " " << "Destructor " << name_ << "\n";
    }
};
int MyValue::counter = 0;        // initialization of the static class variable
```

**Listing 16.3** A destructor is executed when an object is removed.

Equipped like this, you can use the object as usual. To do this, use specific variables of this modified MyValue type in Listing 16.1.

```cpp
// https://godbolt.org/z/enneOWpzb
void function(const MyValue &valueParamRef) {
    MyValue localValue{"local"};
}

int main() {
    MyValue mvalue1{"mvalue1"};
    function( MyValue{"temp"} );
    function( mvalue1 );
    {
        MyValue mvalue2{"mvalue2"};
    }
}
```

**Listing 16.4** Here, many objects are created and destroyed.

Thus, you get the output shown in the following listing.

```text
Constructor mvalue1
  Constructor temp
    Constructor local
    Destructor local
  Destructor temp
    Constructor local
    Destructor local
    Constructor mvalue2
    Destructor mvalue2
Destructor mvalue1
```

**Listing 16.5** This output shows when objects are created and destroyed.

In main, mvalue1 is created first. You used setw to ensure that the first instance of MyValue is indented to a depth of 1, and with ++counter, all subsequent instances are indented one level deeper. The counter value is simultaneously copied into the number_ data field. This way, you can use the same indentation level in the destructor as in the constructor. You can clearly see that mvalue1 is also the last object to be cleaned up: the Destructor mvalue1 output occurs in the destructor.

You also see that temp is created for the function call. Within the function, local is created and removed again—for each of the two calls to function. After returning from the function, temp is removed—at the end of the statement—while mvalue1 remains.

Next, mvalue2 is created. However, the end of the inner block is immediately reached, which is why its destructor is called right after. Only then is the end of main and thus the end of the validity of mvalue1 reached.

### 16.3.1 No Destructor Needed

Normally, it is not necessary to do anything in the destructor because every data field of a class is cleaned up anyway. So if you do nothing, leave the destructor empty, or omit it entirely, all data fields will still be removed.

Just use the mechanisms we've covered so far and you won't need a destructor for cleanup. Basic data types like `int` and `double`, along with standard library types like `string`, `vector`, and `fstream`, manage everything automatically.

### 16.3.2 Resources in the Destructor

But there are resources that are not automatically removed. Raw pointers and many C data types must be handled in the destructor. Alternatively, you can wrap the whole thing in a `shared_ptr` and use a *custom deleter*. You will learn more about this in Chapter 20.

Suppose you are dealing with a database that is provided to you via a library and with the associated header as a programming interface. Simplified, the header might look like the following listing.

```cpp
// https://godbolt.org/z/54dzsb31z
#ifndef DATABASE_HPP
#define DATABASE_HPP

typedef void* db_handle_t;

db_handle_t db_open(const char* filename);
void db_close(db_handle_t db);
int db_execute(db_handle_t db, const char* query);

#endif
```

**Listing 16.6** A simple example of a C interface to a resource.

Thus, it is clear that for every `db_open()`, you must also call a `db_close()`. If you don't, all sorts of things can happen: writes to the database might be forgotten, your program might leak database connections and eventually be unable to perform any more `db_open()`s, or your program might crash.

To ensure that for every `db_open()` a `db_close()` is called, get help from the compiler: constructor calls and destructor calls are always paired. Wrap the resource in a *resource wrapper*.

```cpp
// https://godbolt.org/z/6399qK9Ts
#include <iostream>                 // cout
#include "database.hpp"             // include the foreign API
```
