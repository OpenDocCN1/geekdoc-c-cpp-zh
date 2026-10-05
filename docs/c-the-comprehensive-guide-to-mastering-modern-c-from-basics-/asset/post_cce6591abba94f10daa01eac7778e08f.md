
```cpp
int main() {
    int a = 3;
    int b = 7 + (a = 12) + 6; // contains an assignment
    std::cout << a << std::endl;
}
```

**Listing 4.14** An assignment is an expression with the type of the assigned variable.

Here, a = 12 is the assignment. When executed, this expression has the value 12 and for the compiler the type of a—that is, int. The variable b is therefore initialized with the calculation 7 + 12 + 6.

You should not take this as an example and use assignments as expressions everywhere. The assignment then becomes an expression with a side effect if, in addition to the main effect—changing another variable changes its value. We will later show you the few places where this is common in C++ and therefore there will be no surprises when reading and understanding.

# Value versus Reference

In some programming languages, each variable is only a reference to an object. In Smalltalk, for example, this applies to all variables and in Java to everything that is derived from Object. There, an assignment does not change the object itself, but only assigns another reference. For example, if you have string s = "a"; string t = "b"; in Java, then s = t; is an assignment. Now s and t “point” to the same string object.

This is different in C++: an assignment is always made to the value of a variable. If you have string s = "a"; string t = "b"; in C++, then the assignment s = t; copies the values of the variables. Without further precautions, you always work with values in C++, not with references. Yes, you can also work with references in C++, but you must make this clear. As you'll learn later, then you use & for references and for pointers and addresses.

# 4.2.9 Types

Variables and constants have a type, do parameters and functions, data, classes, and expressions. Types are everywhere.

The type determines how much memory the computer must provide for a variable or the intermediate result of an expression, what kind of values it can hold, how these values are to be interpreted in memory, and what operations are permitted on them.

The latter is a strength of C++. This is because the main work of the compiler consists of processing the type information. First, it determines the type and finds out which things are permitted for this type. These can be function calls, operations, or conversions. What is meant by this program code? When the compiler finds this out, it applies its selection and determines the type for the expression.

This is why type and value always belong together: they complement each other. Conceptually, the type only exists at translation time, as a tool for the compiler.

When you start the translated program (runtime), the types have disappeared and only the values exist. So your program manipulates the values, and the compiler manipulates the types. Through its calculations, the compiler ensures that the desired operations on the values end up in the program.

You can determine the exact type of each (partial) expression. This depends on the operator and its operands. Sometimes it is easy to determine the type, sometimes not, but it is always possible. If it is difficult, you can get help from the computer. The right program for this is the C++ compiler! This is because it “calculates” the types of the expressions according to the rules specified by the C++ standard and your program.

If you already know other programming languages, then you may be familiar with less stringent type concepts than those of C++. Some languages (such as Python, PHP, or JavaScript) ignore them almost completely and work well in their respective domains. Other languages (such as Java or C) have types but see their use somewhat differently. In C++, you are much more likely to use types to let the compiler help you write a correct program.

For example, if the program says 100+99 somewhere, then for the compiler this is an operator + with two operands 100 and 99, each of type int. According to the rules that the compiler has built in, a + with two operands again results in a value of type int, and therefore the overall expression also has the type int. At this point, the compiler does not calculate with the concrete numbers 100 and 99 and does not yet know anything about the meaning of +, but it only applies knowledge “about” operands and operators—their types.

If you had the right teacher in physics lessons at school, this may sound familiar to you. To check whether your result was probably correct when dealing with long formulas, you could only calculate with the units of measurement and quantities instead of the concrete numbers (“dimensional analysis”). If you came up with the wrong unit of measurement, you had made a mistake in the calculation or checking.

For example:

Force in $[kg \times \frac{m}{s^2}] = \frac{Mass \ in [kg] \times Length \ in [m]}{Time \ in [s^2]}$

If you now want to know how much force is acting for a given mass of 8 kg, length of 12 m, and time of 4 s, then calculate $8 \cdot 12/4 = 24$ and kg $\times$ m/s at the same time and realize: “Oops, something’s wrong with the seconds!” The correct calculation would have been $8 \cdot 12/4^2 = 6$, with the check kg $\times$ m/s^2$; that fits.

The compiler does something similar. You specify the rules of the calculation on types through the classes, functions, and templates of your program. These are supplemented by the standard library and other libraries that you use, as well as by the built-in Rules. And just as dimensional analysis helped you in the physics exam, the compiler can help you to write a correct program by

```cpp
// https://godbolt.org/z/9943MfExc
#include <vector>
class Image {
  std::vector<char> data;
  public:
    void load(const char* filename); // loads image data
};
class Screen {
  public:
    void show(Image& image); // N image should be const
  };
void paint(Screen&screen, const Image& image) {
    screen.show(image);
  }
};
int main() {
  Image image;
  image.load("peter.png");
  Screen screen;
  paint(screen, image);
}
```

**Listing 4.15** The compiler helps to write correct programs by checking the types.

The omission of “the power of 2” in C++ corresponds perhaps to a missing const: the screen Screen has a method show with the image. The omission of “the power of 2” in C++ corresponds perhaps to a missing const: the screen Screen has a method show with the image. The omission of “the power of 2” in C++ corresponds perhaps to a missing const: the screen Screen has a method show with the image. The omission of “the power of 2” in C++ corresponds perhaps to a missing const: the screen Screen has a method show with the image. The omission of “the power of 2” in C++ corresponds perhaps to a missing const: the screen Screen has a method show with the image. The omission of “the power of 2” in C++ corresponds perhaps to a missing const: the screen Screen has a method show with the image. The omission of “the power of 2” in C++ corresponds perhaps to a missing const: the screen Screen has a method show with the image. The omission of “the power of 2” in C++ corresponds perhaps to a missing const: the screen Screen has a method show with the image. The omission of “the power of 2” in C++ corresponds perhaps to a missing const: the screen Screen has a method show with the image. The omission of “the power of 2” in C++ corresponds perhaps to a missing const: the screen Screen has a method show with the image. The omission of “the power of 2” in C++ corresponds perhaps to a missing const: the screen Screen has a method show with the image. The omission of “the power of 2” in C++ corresponds perhaps to a missing const: the screen Screen has a method show with the image. The omission of “the power of 2” in C++ corresponds perhaps to a missing const: the screen Screen has a method show with the image. The omission of “the power of 2” in C++ corresponds perhaps to a missing const: the screen Screen has a method show with the image. The omission of “the power of 2” in C++ corresponds perhaps to a missing const: the screen Screen has a method show with the image. The omission of “the power of 2” in C++ corresponds perhaps to a missing const: the screen Screen has a method show with the image. The omission of “the power of 2” in C++ corresponds perhaps to a missing const: the screen Screen has a method show with the image. The omission of “the power of 2” in C++ corresponds perhaps to a missing const: the screen Screen has a method show with the image. The omission of “the power of 2” in C++ corresponds perhaps to a missing const: the screen Screen has a method show with the image. The omission of “the power of 2” in C++ corresponds perhaps to a missing const: the screen Screen has a method show with the image. The omission of “the power of 2” in C++ corresponds perhaps to a missing const: the screen Screen has a method show with the image. The omission of “the power of 2” in C++ corresponds perhaps to a missing const: the screen Screen has a method show with the image. The omission of “the power of 2” in C++ corresponds perhaps to a missing const: the screen Screen has a method show with the image. (Note: skipping repetitive OCR artifacts)

The omission of “the power of 2” in C++ corresponds perhaps to a missing const: the screen Screen has a method show with the image. The omission of “the power of 2” in C++ corresponds perhaps to a missing const: the image. The omission of “the power of 2” in C++ corresponds perhaps to a missing const: the screen Screen has a method show with the image. The omission of “the power of 2” in C++ corresponds perhaps to a missing const: the screen Screen has a method show with the image. The omission of “the power of 2” in C++ corresponds perhaps to a missing const: the screen Screen has a method show with the image. The omission of “the power of 2” in C++ corresponds perhaps to a missing const: the screen Screen has a method show with the image. The omission of “the power of 2” in C++ corresponds perhaps to a missing const: the screen Screen has a method show with the image. The omission of “the power of 2” in C++ corresponds perhaps to a missing const: the screen Screen has a method show with the image. The omission of “the power of 2” in C++ corresponds perhaps to a missing const: the screen Screen has a method show with the image. The omission of “the power of 2” in C++ corresponds perhaps to a missing const: the screen Screen has a method show with the image. The omission of “the power of 2” in C++ corresponds perhaps to a missing const: the screen Screen has a method show with the image. The omission of “the power of 2” in C++ corresponds perhaps to a missing const: the screen Screen has a method show with the image.

The omission of “the power of 2” in C++ corresponds perhaps to a missing const: the screen Screen has a method show with the image. The omission of “the power of 2” in C++ corresponds perhaps to a missing const: the image. The omission of “the power of 2” in C++ corresponds perhaps to a missing const: the screen Screen has a method show with the image. The omission of “the power of 2” in C++ corresponds perhaps to a missing const: the screen Screen has a method show with the image. (OCR cleanup)

You should use type safety wherever you can. It represents one of the most powerful advantages of C++ over old C. There, the transformations possible (and are) much restricted.

![](img/290cf954ad53865de98cca8e6f_140)

First Simple Types
Without perhaps realizing it, you have already dealt with all kinds of types in the examples. We will now cover the most important ones.

# The "int" Type

In this chapter, int is a representative of all types you can use in C++ to represent integers—that is, negative integers, zero, and positive integers. However, a computer has limitations when it comes to its number range. With int, you have a different number of bits depending on the system. If you are working on a current system, it is probably 32 bits, but it could be 16, 64, or a completely different number. With 32 bits, int can store integers from about -2 billion to +2 billion. You can find out exactly with Listing 2.29. If you want to cover other number ranges, you should take a closer look at the relatives char and short as well as long and long long in Section 4.4.

# The "bool" Type

While an int variable can assume many states, a bool variable is fixed to one of two states: true
Or false. 

```cpp
// https://godbolt.org/z/zK9Ke porównn48
#include <iostream> // cout
int main(int argc, const char* argv[]) { // comparison result stored
    bool withParameters = argc > 1;
    if(withParameters) // ... and used
        std::cout << "You have called the program with parameters\n";
    return 0;
}
```

**Listing 4.16** Variables of type bool can store the result of a comparison.

# The Types "const char*" and "std::string"

These two very different types have the same purpose: their variables represent strings—that is, text strings, like texts, messages, notes, names, and so on. Depending on the task, sometimes the "pointer variant" const char*, which cannot deny its origin in C, is suitable, and sometimes the std::string "class" from the C++ standard library is suitable.

> Pointers, Addresses, and Memory Areas

Note the asterisk * in char* or const char*. This tells you: "I am only storing the address of something." This means that there is a char where the variable
