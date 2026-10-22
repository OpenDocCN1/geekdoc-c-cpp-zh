after the template name: [Click here to view code image](#)

```
template<typename T> class Box; // OK: primary template
template<typename T> class Box<T>; // ERROR: does not specialize

template<typename T> void translate(T); // OK: primary template
template<typename T> void translate<T>(T); // ERROR: not allowed for functions

template<typename T> constexpr T zero = T{}; // OK: primary template
template<typename T> constexpr T zero<T> = T{}; // ERROR: does not specialize
```

Nonprimary templates occur when declaring *partial specializations* of class or variable templates. Those are discussed in [Chapter 16](#). Function templates must always be primary templates (see [Section 17.3 on page 356](#) for a discussion of a potential future language change).

# 12.2 Template Parameters

There are three basic kinds of template parameters:

+   1. Type parameters (these are by far the most common)
+   2. Nontype parameters
+   3. Template template parameters
+   
+   Any of these basic kinds of template parameters can be used as the basis of a *template parameter pack* (see Section 12.2.4 on page 188).

Template parameters are declared in the introductory parameterization clause of a template declaration.¹ Such declarations do not necessarily need to be named: [Click here to view code image](#)

```
template<typename, int>
class X; // X<> is parameterized by a type and an integer
```

A parameter name is, of course, required if the parameter is referred to later in the template. Note also that a template parameter name can be referred to in a subsequent parameter declaration (but not before): [Click here to view code image](#)

```
template<typename T, // the first parameter is used
         T Root, // in the declaration of the second one and
template<T> class Buf> // in the declaration of the third one
class Structure;
```

# 12.2.1 Type Parameters