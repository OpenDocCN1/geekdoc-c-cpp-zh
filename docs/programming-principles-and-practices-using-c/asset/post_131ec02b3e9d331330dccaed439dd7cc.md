
## Naming and layout

**R300:** Indentations shall be used and be consistent within the same source file.
*Reason:* Readability and style.

**R301:** Each new statement starts on a new line.
*Reason:* Readability.

```cpp
// Example:
int a = 7; x = a+7; f(x,9); // violation
int a = 7; // OK
x = a+7; // OK
f(x,9); // OK
```

```cpp
// Example:
if (p<q) cout << *p; // violation
```

```cpp
// Example:
if (p<q)
  cout << *p; // OK
```

**R302:** Identifiers should be given descriptive names.
- Identifiers may contain common abbreviations and acronyms.
- When used conventionally, **x, y, i, j**, etc. are descriptive.
- Use the `number_of_elements` style rather than the `numberOfElements` style.
- Hungarian notation shall not be used.
- Type, template, and namespace names (only) start with a capital letter.
- Avoid excessively long names.
- *Example:* `Device_driver` and `Buffer_pool`.
*Reason:* Readability.
*Note:* Identifiers starting with an underscore are reserved to the language implementation by the C++ standard and thus banned.
*Exception:* When calling an approved library, the names from that library may be used.

**R303:** Identifiers shall not differ only by
- A mixture of case
- The presence/absence of the underscore character
- The interchange of the letter **O** with the number 0 or the letter **D**
- The interchange of the letter **I** with the number 1 or the letter **l**
- The interchange of the letter **S** with the number 5
- The interchange of the letter **Z** with the number 2
- The interchange of the letter **n** with the letter **h**
*Example:* `Head and head` || violation
*Reason:* Readability.

**R304:** No identifier shall be in all capital letters and underscores.
*Example:* `BLUE and BLUE_CHEESE` || violation
*Reason:* All capital letters are widely used for macros that may be used in `#include` files for approved libraries.
*Exception:* Macro names used for `#include` guards.

## Function and expression rules

**R400:** Identifiers in an inner scope should not be identical to identifiers in an outer scope.
*Example:*
`int var = 9; { int var = 7; ++var; }` || violation: var hides var
*Reason:* Readability.

**R401:** Declarations shall be declared in the smallest possible scope.
*Reason:* Keeping initialization and use close minimizes chances of confusion; letting a variable go out of scope releases its resources.

**R402:** Variables shall be initialized.
*Example:*
`int var;` || violation: var is not initialized
*Reason:* Uninitialized variables are a common source of errors.
*Exception:* A variable that is immediately filled from input need not be initialized.
*Note:* Many types, such as `vector` and `string`, have a default constructor to guarantee initialization.

**R403:** Casts shall not be used.
*Reason:* Casts are a common source of errors.
*Exception:* **dynamic_cast** may be used.
*Exception:* Named casts may be used to convert hardware addresses into pointers and **void\*** received from sources external to a program (e.g., a GUI library) into pointers of a proper type.

**R404:** Built-in arrays shall not be used in interfaces; that is, a pointer as function argument shall be assumed to point to a single element. Use **Array_ref** to pass arrays.
*Reason:* An array is passed as a pointer and its number of elements is not carried along to the called function. Also, the combination of implicit array-to-pointer conversion and implicit derived-to-base conversion can lead to memory corruption.

## Class rules

**R500:** Use **class** for classes with no public data members. Use **struct** for classes with no private data members. Don't use classes with both public and private data members.
*Reason:* Clarity.

**R501:** If a class has a destructor or a member of pointer or reference type, it must have a copy constructor and a copy assignment defined or prohibited.
*Reason:* A destructor usually releases a resource. The default copy semantics rarely does “the right thing” for pointer and reference members or for a class with a destructor.

**R502:** If a class has a virtual function it must have a virtual destructor.
*Reason:* A class has a virtual function so that it can be used through a base class interface. A function that knows an object only through that base class may delete it and derived classes need a chance to clean up (in their destructors).

**R503:** A constructor that accepts a single argument must be declared **explicit**.
*Reason:* To avoid surprising implicit conversions.

## Hard real-time rules

**R800:** Exceptions shall not be used.
*Reason:* Not predictable.

**R801:** `new` shall be used only during startup.
*Reason:* Not predictable.
*Exception:* Placement-`new` (with the standard meaning) may be used for memory allocated from stacks.

**R802:** `delete` shall not be used.
*Reason:* Not predictable; can cause fragmentation.

**R803:** `dynamic_cast` shall not be used.
*Reason:* Not predictable (assuming common implementation technique).

**R804:** The standard library containers, except `std::array`, shall not be used.
*Reason:* Not predictable (assuming common implementation technique).

## Critical systems rules

**R900:** Increment and decrement operations shall not be used as sub-expressions.
*Example:*
```cpp
int x = v[++i]; // violation
```
*Example:*
```cpp
++i;
int x = v[i]; // OK
```
*Reason:* Such an increment might be overlooked.

**R901:** Code should not depend on precedence rules below the level of arithmetic expressions.
*Example:*
```cpp
x = a*b+c; // OK
```
*Example:*
```cpp
if (a<b || c<=d) // violation: parenthesize(a<b) and (c<=d)
```
*Reason:* Confusion about precedence has been repeatedly found in code written by programmers with a weak C/C++ background.

We left gaps in the numbering so that we could add new rules without changing the numbering of existing ones and still have the general classification recognized through the numbering. It is very common for rules to become known by their number, so that renumbering would be resisted by the users.

### 25.6.3 Real coding standards

There are lots of C++ coding standards. Most are corporate and not widely available. In many cases, that’s probably a good thing except possibly for the programmers of those corporations. Here is a list of standards that – when used appropriately in areas to which they apply – can do some good:

- Google C++ Style Guide: http://google-styleguide.googlecode.com/svn/trunk/cppguide.xml. A rather old-style and restrictive but evolving style guide.
- Lockheed Martin Corporation. *Joint Strike Fighter Air Vehicle Coding Standards for the System Development and Demonstration Program*. Document Number 2RDU00001 Rev C. December 2005. Colloquially known as “JSF++”; a set of rules written at Lockheed-Martin Aero for air vehicle (read “airplane”) software. These rules really were written by and for programmers who produce software upon which human lives depend. www.stroustrup.com/JSF-AV-rules.pdf.
- Programming Research. High-integrity C++ Coding Standard Manual Version 2.4. www.programmingresearch.com.
- Sutter, Herb, and Andrei Alexandrescu. *C++ Coding Standards: 101 Rules, Guidelines, and Best Practices*. Addison-Wesley, 2004. ISBN 0321113586. This is more of a “meta coding standard”; that is, instead of specific rules it has guidance on which rules are good and why.

Note that there is no substitute for knowing your application area, your programming language, and the relevant programming technique. For most applications – and certainly for most embedded systems programming – you also need to know your operating system and/or hardware architecture. If you need to use C++ for low-level coding, have a look at the ISO C++ committee’s report on performance (ISO/IEC TR 18015, www.stroustrup.com/performanceTR.pdf); by “performance” they/we primarily mean “embedded systems programming.”

Language dialects and proprietary languages abound in the embedded systems world, but whenever you can, use standardized language (such as ISO C++), tools, and libraries. That will minimize your learning curve and increase the likelihood that your work will last.
