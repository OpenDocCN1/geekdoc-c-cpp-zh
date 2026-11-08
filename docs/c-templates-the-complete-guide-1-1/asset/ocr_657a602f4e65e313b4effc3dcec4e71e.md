LE conatger (claasifier<T>)

- -

or, by using partial specializations

Click here to view code image

```
~~~cpp
template<typename T>
class Classifier<T, bool> : public Classifier<T>       //partial specialization for
{                                                      //the general case
};
~~~
```

Furthermore, expressions such as IsDefaultConstructible will be Boolean constants that yield unique template arguments. In turn, powerful template metaprogramming and even some powerful templates that specialize their behavior on the properties of their type arguments.

The C++ standard library defines several similar traits to determine the primary and composite type categories of a type. See Section D.2.1 on page 782 and Section D.2.2 on page 785 for details.

# 9.1.8 Determining Fundamental Types

To start, let's develop a template to determine whether a type is a fundamental type. By default, a type is not fundamental, and we specialize the template for the fundamental types.

Click here to view code image

```
~~~cpp
template<typename T>      // for multiplies, T
struct IsFundaT : std::false_type {
};

// primary template: in general T is not a fundamental type
template<typename T>
struct IsFundaT : std::false_type {
};

// macro to specialize for fundamental types
#define MK_FUNDA_TYPE(T) \
  template<> struct IsFundaT<T> : std::true_type { \
  };

MK_FUNDA_TYPE(void)
MK_FUNDA_TYPE(bool)
MK_FUNDA_TYPE(char)
MK_FUNDA_TYPE(signed char)
MK_FUNDA_TYPE(unsigned char)
MK_FUNDA_TYPE(wchar_t)
MK_FUNDA_TYPE(char16_t)
MK_FUNDA_TYPE(char32_t)

MK_FUNDA_TYPE(signed short)
MK_FUNDA_TYPE(unsigned short)
MK_FUNDA_TYPE(signed int)
MK_FUNDA_TYPE(unsigned int)
MK_FUNDA_TYPE(signed long)
MK_FUNDA_TYPE(unsigned long)
MK_FUNDA_TYPE(signed long long)
MK_FUNDA_TYPE(unsigned long long)

MK_FUNDA_TYPE(float)
~~~
```