
explicitly calls the base class constructor, passing it t. This base class initialization expression must be the first thing in the initialization list because C++ requires that the parts of an object inherited from its base class must be initialized before any new parts (added by the derived class) are initialized. The next three expressions in the initialization list:

```
... left_bracket(left), right_bracket(right), connector(conn) ...
```

initialize the left_bracket, right_bracket, and connector fields of the FancyText object under construction. The body of the constructor is empty as no other initialization work is necessary.

The FancyText class alters the way get works. We say the FancyText class overrides its inherited get method. The keyword override emphasizes the fact that the code in the get method in FancyText intends to do something differently from the code in Text's get method. In this case FancyText::get method builds a string result by concatenating three other strings: the first string is a front bracketing string, the second is the wrapped string, and the third string is a trailing bracketing string. Notice that the second string is obtained with the expression

```
Text::get()
```

This calls the base class version of the get method. We say that the FancyText::get method delegates some of its work to the base class version, Text::get. Notice that the statement

```
return left_bracket + text + right_bracket; // Illegal
```

would be illegal because text is private to the base class. The member specifier private means inaccessible outside of the class, period. Derived classes have no special privilege in this regard. In order to perform the delegation we must use Text::get() and not simply get(); the unqualified expression get() is equivalent to this->get, which calls FancyText::get. This means invoking the unqualified get within the definition FancyText::get is a recursive call, which is not what we want.

A method declared virtual in a base class is automatically virtual in its derived classes. You may repeat the virtual specifier in derived classes, but the use of override makes this redundant.

![](img/e84ad11adb18201d71595b31ce6c9eff_513_0.png)

The override keyword was added to the language in C++11. Prior to C++11 when a method in a derived class had the same signature as a virtual method in its base class, the method implicitly overrode its base class version. The problem was that a programmer could intend to override a method in the derived class but get the signature wrong. The resulting method overloaded the original method rather than overriding it. If a programmer uses the override specifier and uses a signature that does not match the base class version, the compiler will report an error. The override specifier provides a way for programmers to explicitly communicate their intentions.

For backwards compatibility the override keyword is optional. Its presence enables the compiler to verify that the method is actually overriding a virtual method in the base class. Without it, the programmer must take care to faithfully reproduce the signature of the method to override.

The override keyword is a context-sensitive keyword, meaning it is a keyword only when appearing as it does here in the declaration of a method header. In other contexts it behaves like an identifier.

The FancyText::append method overrides the inherited append method by inserting a special separator string in between the existing wrapped text string and the string to append. Like FancyText::get, the FancyText::append method delegates the actual concatenation operation to its base class by calling Text::append. Again, this is because code within the FancyText class cannot directly influence its text field.

The class FixedText, declared and defined in Listing 17.6 (fixedtext.h) and Listing 17.7 (fixedtext.cpp), is another class derived from Text.

```cpp
#ifndef FIXEDTEXT_H_INCLUDED
#define FIXEDTEXT_H_INCLUDED

// Compiler needs to know specifics of the Text class in order to
// derive a new class from it
#include "text.h"

// The text is always the word FIXED
class FixedText: public Text {
public:
    // Client does not provide a string argument; the
    // wrapped text is always "FIXED"
    FixedText();

    // Nothing may be appended to a FixedText object
    void append(const std::string&) override;
};

#endif
```

The FixedText class is somewhat simpler than the FancyText class. It adds no fields and does not override the get method. Its constructor accepts no parameters because clients are not permitted to determine the contents of the wrapped string—the text field is always the word FIXED. It inherits the text field and get method (as is) from the Text class.

```cpp
#include "fixedtext.h"

// Client does not provide a string argument; the
// wrapped text is always "FIXED"
FixedText::FixedText(): Text("FIXED") {}

// Nothing may be appended to a FixedText object
void FixedText::append(const std::string&) {
    // Disallow concatenation
}
```

The FixedText constructor implementation invokes the base class constructor to assign the string "FIXED" to its inherited text field. The get method needs no customization. The custom append method does nothing, as clients are not allowed to add any extra text.

Listing 17.8 (testtext.cpp) exercises these classes.

## Listing 17.8: testtext.cpp

```cpp
#include <iostream>
#include "text.h"
#include "fancytext.h"
#include "FixedText.h"

int main() {
    Text t1("plain");
    FancyText t2("fancy", "<<", ">>", "***");
    FixedText t3;
    std::cout << t1.get() << " ' \n";
    std::cout << t2.get() << " ' \n";
    std::cout << t3.get() << " ' \n";
    std::cout << "-----------------------------------\n";
    t1.append("A");
    t2.append("A");
    t3.append("A");
    std::cout << t1.get() << " ' \n";
    std::cout << t2.get() << " ' \n";
    std::cout << t3.get() << " ' \n";
    std::cout << "-----------------------------------\n";
    t1.append("B");
    t2.append("B");
    t3.append("B");
    std::cout << t1.get() << " ' \n";
    std::cout << t2.get() << " ' \n";
    std::cout << t3.get() << " ' \n";
}
```

The output of Listing 17.8 (testtext.cpp) is

```
plain
<<fancy>>
FIXED
--------------------------------
plainA
<fancy***A>
FIXED
--------------------------------
plainAB
<fancy***A***+B>
FIXED
```

Given the Text and FancyText classes as declared in Listing 17.2 (text.h) and Listing 17.5 (fancytext.cpp), the following client code is legal:

```
Text t1("ABC");
FancyText t2("XYZ", "[", "]", ":=");
std::cout << t1.get() << " " << t2.get() << " \n";
t1 = t2;
std::cout << t1.get() << " " << t2.get() << " \n";
```

Since t2's declared type is FancyText, by virtue of inheritance, t2 is a Text object as well. The above code fragment prints

## Figure 17.1 Object slicing during assignment of a derived class instance to a base class variable

```
Text t1("plain");
FancyText t2("Fancy", "<<", ">>", "::");
```

![](img/e84ad11adb18201d71595b31ce6c9eff_516_0.png)

```
t1 = t2;
```

![](img/e84ad11adb18201d71595b31ce6c9eff_516_1.png)

```
ABC <<XYZ>>
XYZ <<XYZ>>
```

Notice that the assignment

```
t1 = t2;
```

copied into object t1 only the fields that FancyText objects have in common with Text objects; that is, the text field. Since t1 is a plain Text object, it does not have the left_bracket, right_bracket, and connector fields capable of storing the additional data contained in a FancyText object. This process of losing derived class data when assigning to a base class instance is known as object slicing. The parts that will not fit into the base class instance are “sliced” off. Figure 17.1 illustrates object slicing.

Note that the assignment in the other direction:

```
t2 = t1; // Illegal
```

is not possible; even though any FancyText object is a Text object, we cannot say any Text object is a FancyText object (it could be a FixedText object or just a Text object without any special decoration). Figure 17.2 shows how such an attempted assignment would be meaningless because the base class instance has missing information needed by the derived class instance. Failure to properly assign all
