# ISO/IEC 14882:2017(E)

# 7.3 Function-to-pointer conversion [conv.func]

1 An value of type T can be converted to a pointer of type "pointer to T". The result is a pointer to the function.<sup>59}

2 [Note: See 16.4 for additional rules for the case where the function is overloaded. — end note]

# 7.4 Temporaryization conversion [conv.rav]

1 A value of type T can be converted to an xvalue of type T. This conversion initializes a temporary object (15.2) of type T from the prvalue by evaluating the prvalue as its result object, and produces an xvalue denoting the temporary. T must be a complete type. [Note: If T is a class type (or array thereof), it must have an accessible and non-destructive destructor; See 15.4. — end note]

```
struct X { int n; }
int k = x; // OK, xvalue is converted to xvalue
// end example
```

# 7.5 Qualification conversion [conv.qual]

+   1 A de-composition of type T is a sequence of cv<sub>i</sub> P<sub>i</sub> such that T is
   -cv₀ P₀ · · · cvₙₙ Pₙₙ for n > 0,
   where cv<sub>i</sub> is a cv-qualifier of the element as type (6.9,3), and P<sub>i</sub> is "pointer to" (11.3.1), pointer to member C<sub>i</sub> of type T (11.3.3), "array of n<sub>i</sub>", or of unknown bound of" (11.4). If P<sub>i</sub> designates an array, the cv-qualifiers cv<sub>i+1</sub>=cv<sub>i</sub>,...,cvₙ,, is called the cv-qualification signature of the first in the cv-decomposition of T. [Example: The type denoted by the type-id const int has two cv-qualifications, using as "int" and "pointer to
   const int; — end example]

+   2 Two types T₁ and T₂ are similar if they have cv-qualifiers with the same n such that corresponding P₁ and P₂ are the same and the types denoted by U are the same.

+   3 A expression of type T₁ can be converted to T₂ if the following conditions are satisfied, where cv¹ and cv² are cv-qualifiers of T₁, T₂:

(3.1) For every i > 0, if const is in cv¹ then const is in cv², and similarly for volatile.

(3.3) If the cv¹ and cv² are different, then const is in cv² for 0 < k < i.

[Note: If a program could add a type of T* to pointer T** (that is, if line #1 below were allowed), a program could inadvertently modify a const object (as it is done on line #2). For example:

```
int main() {
  const char c = 'c';
  char* pc;
  char** pacc = &c; // #1: not allowed
  *pc = &c;
*pc = 'C'; // #2: modifies a const object
}
```

— end note

59) This conversion never applies to non-static member functions because an lvalue refers to a non-static member function cannot be obtained.

60) These rules ensure const-safety is preserved by the conversion.

§ 7.5 ©/IEC 2017 – All rights reserved 88