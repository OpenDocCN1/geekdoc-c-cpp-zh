
## Changing the Implementation

There may be something about the program output, aside from Fluffy the Cat’s lack of financial acumen, that bothers you—the somewhat inconsistent formatting of the numbers. Here’s an opportunity to refine an implementation while keeping the interface unchanged. The ostream class includes member functions that control formatting. Without going into much detail, you can avoid e-notation by using the setf() method much as we did in Listing 8.8:

```cpp
std::cout.setf(std::ios_base::fixed, std::ios_base::floatfield);
```

This sets a flag in the cout object instructing cout to use fixed-point notation. Similarly, the following statement causes cout to show three places to the right of the decimal when using fixed-point notation:

```cpp
std::cout.precision(3);
```

You’ll find more details in Chapter 17, “Input, Output, and Files.”

These tools can be used in the show() method to control the formatting, but there is another point to consider. When you change the implementation for a method, the changes should not affect other parts of the client program. The format changes just mentioned stay in place until changed again, so they could affect subsequent output in the client program. Therefore, the polite thing for show() to do is to reset the formatting information to the state that existed before show() was called. This can be done, as in Listing 8.8, using return values for the setting statements:

```cpp
std::streamsize prec =
    std::cout.precision(3);    // save preceding value for precision
...
std::cout.precision(prec);        // reset to old value

// store original flags
std::ios_base::fmtflags orig = std::cout.setf(std::ios_base::fixed);
...
// reset to stored values
std::cout.setf(orig, std::ios_base::floatfield);
```

As you may recall, fmtflags is a type defined in the ios_base class, which is defined in the std namespace, hence the rather long type name for orig. Second, orig holds all the flags, and the reset statement uses that information to reset information in the floatfield section, which includes flags for fixed-point notation and scientific notation. Third, let’s not worry too much about the details here. The main points are that the changes are confined to the implementation file and that the changes don’t affect other aspects of the program using the class.

Putting this information to use, we can replace the `show()` definition in the implementation file with this:

```cpp
void Stock::show()
{
    using std::cout;
    using std::ios_base;
    // set format to #.###
    ios_base::fmtflags orig =
        cout.setf(ios_base::fixed, ios_base::floatfield);
    std::streamsize prec = cout.precision(3);

    cout << "Company: " << company
         << "  Shares: " << shares << '\n';
    cout << "  Share Price: $" << share_val;
    // set format to #.##
    cout.precision(2);
    cout << "  Total Worth: $" << total_val << '\n';

    // restore original format
    cout.setf(orig, ios_base::floatfield);
    cout.precision(prec);
}
```

After this replacement and leaving the header file and client file unchanged, you can recompile the program. Now the output would look like this:

```text
Company: NanoSmart  Shares: 20
  Share Price: $12.500  Total Worth: $250.00
Company: NanoSmart  Shares: 35
  Share Price: $18.125  Total Worth: $634.38
You can't sell more than you have! Transaction is aborted.
Company: NanoSmart  Shares: 35
  Share Price: $18.125  Total Worth: $634.38
Company: NanoSmart  Shares: 300035
  Share Price: $40.125  Total Worth: $12038904.38
Company: NanoSmart  Shares: 35
  Share Price: $0.125  Total Worth: $4.38
```

## Reviewing Our Story to Date

The first step in specifying a class design is to provide a class declaration. The class declaration is modeled after a structure declaration and can include data members and function members. The declaration has a private section, and members declared in that section can be accessed only through the member functions. The declaration also has a public section, and members declared there can be accessed directly by a program using class objects.

Typically, data members go into the private section and member functions go into the public section, so a typical class declaration has this form:

```cpp
class className
{
private:
    data member declarations
public:
    member function prototypes
};
```

The contents of the public section constitute the abstract part of the design, the public interface. Encapsulating data in the private section protects the integrity of the data and is called data hiding. Thus, using a class is the C++ way of making it easy to implement the OOP features abstraction, data hiding, and encapsulation.

The second step in specifying a class design is to implement the class member functions. You can use a complete function definition instead of a function prototype in the class declaration, but the usual practice, except with very brief functions, is to provide the function definitions separately. In that case, you need to use the scope-resolution operator to indicate to which class a member function belongs. For example, suppose the Bozo class has a member function called Retort() that returns a pointer to a char. The function header would look like this:

```cpp
char * Bozo::Retort();
```

In other words, Retort() is not just a type char * function; it is a type char * function that belongs to the Bozo class. The full, or qualified, name of the function is Bozo::Retort(). The name Retort(), on the other hand, is an abbreviation of the qualified name, and it can be used only in certain circumstances, such as in the code for the class methods.

Another way of describing this situation is to say that the name Retort has class scope, so the scope-resolution operator is needed to qualify the name when it is used outside the class declaration and a class method.

To create an object, which is a particular example of a class, you use the class name as if it were a type name:

```cpp
Bozo bozetta;
```

This works because a class is a user-defined type.

You invoke a class member function, or method, by using a class object. You do so by using the dot membership operator:

```cpp
cout << bozetta.Retort();
```

This invokes the Retort() member function, and whenever the code for that function refers to a particular data member, the function uses the value that member has in the bozetta object.

## Class Constructors and Destructors

At this point, you need to do more with the Stock class. There are certain standard functions, called *constructors* and *destructors*, that you should normally provide for a class. Let’s talk about why they are needed and how to write them.

One of C++’s aims is to make using class objects similar to using standard types. However, the code provided so far in this chapter doesn’t let you initialize a Stock object the way you can an ordinary int or struct. That is, the usual initialization syntax doesn’t carry over for the Stock type.

```cpp
int year = 2001;                                  // valid initialization
struct thing
{
    char * pn;
    int m;
};
thing amabob = {"widget", -23};                  // valid initialization
Stock hot = {"Sukie's Autos, Inc.", 200, 50.25};  // NO! compile error
```

The reason you can’t initialize a Stock object this way is because the data parts have private access status, which means a program cannot access the data members directly. As you’ve seen, the only way a program can access the data members is through a member function. Therefore, you need to devise an appropriate member function if you’re to succeed in initializing an object. (You could initialize a class object as just shown if you made the data members public instead of private, but making the data public goes against one of the main justifications for using classes: data hiding.)

In general, it’s best that all objects be initialized when they are created. For example, consider the following code:

```cpp
Stock gift;
gift.buy(10, 24.75);
```

With the current implementation of the Stock class, the gift object has no value for the company member. The class design assumes that the user calls acquire() before calling any other member functions, but there is no way to enforce that assumption. One way around this difficulty is to have objects initialized automatically when they are created. To accomplish this, C++ provides for special member functions, called *class constructors*, especially for constructing new objects and assigning values to their data members. More precisely, C++ provides a name for these member functions and a syntax for using them, and you provide the method definition. The name is the same as the class name. For example, a possible constructor for the Stock class is a member function called Stock(). The constructor prototype and header have an interesting property: Although the constructor has no return value, it’s not declared type void. In fact, a constructor has no declared type.
