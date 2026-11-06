
## Functions and Operators

- 25. **Take parameters appropriately by value, (smart) pointer, or reference.**  
  *Parameterize well:* Distinguish among input, output, and input/output parameters, and between value and reference parameters. Take them appropriately.

- 26. **Preserve natural semantics for overloaded operators.**  
  *Programmers hate surprises:* Overload operators only for good reason, and preserve natural semantics; if that's difficult, you might be misusing operator overloading.

- 27. **Prefer the canonical forms of arithmetic and assignment operators.**  
  *If you `a+b`, also `a+=b`:* When defining binary arithmetic operators, provide their assignment versions as well, and write to minimize duplication and maximize efficiency.

- 28. **Prefer the canonical form of `++` and `--`. Prefer calling the prefix forms.**  
  *If you `++c`, also `c++`:* The increment and decrement operators are tricky because each has pre- and postfix forms, with slightly different semantics. Define `operator++` and `operator--` that mimic the behavior of their built-in counterparts. Prefer to call the prefix versions if you don't need the original value.

- 29. **Consider overloading to avoid implicit type conversions.**  
  *Do not multiply objects beyond necessity (Occam's Razor):* Implicit type conversions provide syntactic convenience (but see Item 40). But when the work of creating temporary objects is unnecessary and optimization is appropriate (see Item 8), you can provide overloaded functions with signatures that match common argument types exactly and won't cause conversions.

- 30. **Avoid overloading `&&`, `||`, or `,` (comma).**  
  *Wisdom means knowing when to refrain:* The built-in `&&`, `||`, and `,` (comma) enjoy special treatment from the compiler. If you overload them, they become ordinary functions with very different semantics (you will violate Items 26 and 31), and this is a sure way to introduce subtle bugs and fragilities. Don't overload these operators natively.

- 31. **Don't write code that depends on the order of evaluation of function arguments.**  
  *Keep (evaluation) order:* The order in which arguments of a function are evaluated is unspecified, so don't rely on a specific ordering.

## Class Design and Inheritance

- 32. **Be clear what kind of class you're writing.**  
  *Know thyself:* There are different kinds of classes. Know which kind you are writing.

- 33. **Prefer minimal classes to monolithic classes.**  
  *Divide and conquer:* Small classes are easier to write, get right, test, and use. They are also more likely to be usable in a variety of situations. Prefer such small classes that embody simple concepts instead of kitchen-sink classes that try to implement many and/or complex concepts (see Items 5 and 6).

- 42. Don’t give away your internals.  
  *Don’t volunteer too much: Avoid returning handles to internal data managed by your class, so clients won’t uncontrollably modify state that your object thinks it owns.*

- 43. Pimpl judiciously.  
  *Overcome the language’s separation anxiety: C++ makes private members inaccessible, but not invisible. Where the benefits warrant it, consider making private members truly invisible using the Pimpl idiom to implement compiler firewalls and increase information hiding. (See Items 11 and 41.)*

- 44. Prefer writing nonmember nonfriend functions.  
  *Avoid membership fees: Where possible, prefer making functions nonmember nonfriends.*

- 45. Always provide **new** and **delete** together.  
  *They’re a package deal: Every class-specific overload **void\* operator new(parms)** must be accompanied by a corresponding overload **void operator delete(void\*, parms)**, where parms is a list of extra parameter types (of which the first is always **std::size_t**). The same goes for the array forms **new[]** and **delete[]**.*

- 46. If you provide any class-specific **new**, provide all of the standard forms (plain, in-place, and nothrow).  
  *Don’t hide good news: If a class defines any overload of **operator new**, it should provide overloads of all three of plain, in-place, and non-throwing **operator new**. If you don’t, they’ll be hidden and unavailable to users of your class.*

## Construction, Destruction, and Copying

- 47. Define and initialize member variables in the same order.  
  *Agree with your compiler: Member variables are always initialized in the order they are declared in the class definition; the order in which you write them in the constructor initialization list is ignored. Make sure the constructor code doesn’t confusingly specify a different order.*

- 48. Prefer initialization to assignment in constructors.  
  *Set once, use everywhere: In constructors, using initialization instead of assignment to set member variables prevents needless run-time work and takes the same amount of typing.*

- 49. Avoid calling virtual functions in constructors and destructors.  
  *Virtual functions only “virtually” always behave virtually: Inside constructors and destructors, they don’t. Worse, any direct or indirect call to an unimplemented pure virtual function from a constructor or destructor results in undefined behavior. If your design wants virtual dispatch into a derived class from a base class constructor or destructor, you need other techniques such as post-constructors.*

- 50. Make base class destructors public and virtual, or protected and nonvirtual.  
  *To delete, or not to delete; that is the question: If deletion through a pointer to a base **Base** should be allowed, then **Base**’s destructor must be public and virtual. Otherwise, it should be protected and nonvirtual.*

- 51. **Destructors, deallocation, and swap never fail.**  
  *Everything they attempt shall succeed: Never allow an error to be reported from a destructor, a resource deallocation function (e.g., **operator delete**), or a swap function. Specifically, types whose destructors may throw an exception are flatly forbidden from use with the C++ standard library.*

- 52. **Copy and destroy consistently.**  
  *What you create, also clean up: If you define any of the copy constructor, copy assignment operator, or destructor, you might need to define one or both of the others.*

- 53. **Explicitly enable or disable copying.**  
  *Copy consciously: Knowingly choose among using the compiler-generated copy constructor and assignment operator, writing your own versions, or explicitly disabling both if copying should not be allowed.*

- 54. **Avoid slicing. Consider Clone instead of copying in base classes.**  
  *Sliced bread is good; sliced objects aren't: Object slicing is automatic, invisible, and likely to bring wonderful polymorphic designs to a screeching halt. In base classes, consider disabling the copy constructor and copy assignment operator, and instead supplying a virtual **Clone** member function if clients need to make polymorphic (complete, deep) copies.*

- 55. **Prefer the canonical form of assignment.**  
  *Your assignment: When implementing **operator=**, prefer the canonical form—nonvirtual and with a specific signature.*

- 56. **Whenever it makes sense, provide a no-fail swap (and provide it correctly).**  
  *swap is both a lightweight and a workhorse: Consider providing a **swap** function to efficiently and infallibly swap the internals of this object with another's. Such a function can be handy for implementing a number of idioms, from smoothly moving objects around to implementing assignment easily to providing a guaranteed commit function that enables strongly error-safe calling code. (See also Item 51.)*

## Namespaces and Modules

- 57. **Keep a type and its nonmember function interface in the same namespace.**  
  *Nonmembers are functions too: Nonmember functions that are designed to be part of the interface of a class **X** (notably operators and helper functions) must be defined in the same namespace as the **X** in order to be called correctly.*

- 58. **Keep types and functions in separate namespaces unless they're specifically intended to work together.**  
  *Help prevent name lookup accidents: Isolate types from unintentional argument-dependent lookup (ADL, also known as Koenig lookup), and encourage intentional ADL, by putting them in their own namespaces (along with their directly related nonmember functions; see Item 57). Avoid putting a type into the same namespace as a templated function or operator.*

- 59. **Don't write namespace usings in a header file or before an #include.**  
  *Namespace usings: are for your convenience, not for you to inflict on others: Never write a **using** declaration or a **using** directive before an **#include** directive.*
