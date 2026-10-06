# ISO/IEC 14882:2017(E)

to-function conversion function, or a reference-to-function conversion function on a class object named in the function syntax (16.3.1.2);

+   (2.3) invocation of the operator referenced in an expression (16.3.1.2);

+   (2.4) invocation of a constructor for default- or de-initialization (11.6) of a class objects (16.3.1.3);

+   (2.5) invocation of a user-defined constructor for copy-initialization (11.6) of a class object (16.3.1.4);

+   (2.6) invocation of a conversion function for initialization of an object of a non-class type by an expression of class type (16.3.1.5); and

+   (2.7) invocation of a conversion function to a guise or class value to which (11.6.3) will be directly direct (16.3.1.6).

Each of these contexts defines the set of candidates and the list of arguments in its unique way. But, once the candidate functions and lists have been identified, the selection of the best function is the same in all cases:

+   (2.8) First, a subset of the candidate functions (that have the proper number of arguments and meet other conditions) is selected to form a set of viable functions (16.3.2).

Then the best viable function is selected based on implicit conversion sequences (16.3.3.1) to match each argument to the parameter of each viable function,

3 If a best viable function exists and is unique, overload resolution succeeds and produces it the result. Overload resolution fails and the overload is ill-formed. When overload resolution succeeds, and the best function is not ambiguous (Clause 14) in the context in which it is used, the program is ill-formed.

# 16.3.1 Candidate functions and argument lists [over.match.funcs]

+   1 The subclause of 16.3.1 describe the set of candidate functions and the argument list submitted to overload in each context where overload resolution is. The source transformations and constructions defined in these subclause are only for the purpose of describing the overload process. Implementation is not required to use such transformations and constructions.

+   2 The set of functions can contain both member and non-member functions to be resolved within the same argument list. For an object context, a member function is considered to have an extra parameter, the implicit object parameter, and static and non-static member functions have an implicit object parameter, but constructors do not.

+   3 Similarly, when appropriate, the context can construct an argument list that contains an implicit object parameter to match the object to which the function is called. The parameters are associated by position within their respective lists, and the implicit object parameter, if present, is always the first argument.

+   4 For non-member functions, the type of the implicit object parameter is

+   (4.1) "value reference to cv" for functions declared without a ref-qualifier or with the & ref-qualifier

+   (4.2) "value reference to cv X" for functions declared with the && ref-qualifier

where X is the class of the function member and cv is the cv-qualification on the member function. [Example: For a const member function of class X, the extra parameter is assumed to have type "reference to const X"; — end example]. For conversion functions, the function is considered to be a member of the class of the implicit object parameter. For non-conversion functions introduced by a using-declaration into a derived class, the function is considered to be a member of the derived class for the purpose of defining the type of the implicit object parameter. For static member functions, the implicit object parameter is considered to match

§ 16.3.1

©ISO/IEC 2017 – All rights reserved

313