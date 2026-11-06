# Section 10.12 Converting Between Types

+   - The compiler cannot know in advance how to convert among user-defined types, and between user-defined types and fundamental types, so you must specify how to do this. Such conversions can be performed with **conversion constructors** (p. 481)—single-argument constructors that turn objects of other types (including fundamental types) into objects of a particular class.
+   - A constructor that can be called with a single argument can be used as a conversion constructor.
+   - A **conversion operator** (p. 481) must be a non-`static` member function. Overloaded **cast-operator functions** (p. 481) can be defined for converting objects of user-defined types into fundamental types or into objects of other user-defined types.
+   - An overloaded cast operator function does not specify a return type—the return type is the type to which the object is being converted.
+   - When necessary, the compiler can call cast operators and conversion constructors implicitly.