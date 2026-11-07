3 (True/False) With operator overloading, you can have a program containing a function that explicitly takes no arguments and a function of the same name that contains all default arguments.

**Answer:** False. This would cause a compilation error, as the compiler would not know which version of the function to choose to satisfy a call with no arguments.

# 5.15 Function Templates

Overloaded functions typically perform similar operations on different data types. If the program logic and operations are identical for each data type, overloading may be performed more compactly and conveniently with function templates. You write a single function template definition, and C++ automatically generates separate function template specializations (also called template instantiations) to appropriately handle each type of call for the provided argument types. Thus, a single function template defines a family of overloaded functions. Programming with templates is also known as generic programming. In this section, we define a custom function template. In subsequent chapters, you’ll use many C++ standard library templates, and in Chapter 15, we’ll discuss defining custom templates in detail.

# maximum Function Template

Figure 5.12 defines a maximum function template that returns the largest of three values. All function template definitions begin with the **template** keyword (line 3) followed by a template parameter list enclosed in angle brackets (< and >). Every parameter in the template parameter list is preceded by keyword **typename** or keyword **class** (they are synonyms in this context). The type parameters are placeholders for fundamental types or user-defined types. These placeholders—in this case, T—are used to specify the types of the function’s parameters (line 4), to specify the function’s return type (line 4) and to declare variables within the body of the function definition (line 5). A function template is defined like any other function but uses the type parameters as placeholders for actual data types.

```
```cpp
// Fig. 5.12: maximum.h
// Function template maximum header.
template <typename T> // or template <class T>
T maximum(T value1, T value2, T value3) {
   T maximumValue{value1}; // assume value1 is maximum

   // determine whether value2 is greater than maximumValue
   if (value2 > maximumValue) {
      maximumValue = value2;
   }

   // determine whether value3 is greater than maximumValue
   if (value3 > maximumValue) {
      maximumValue = value3;
   }

   return maximumValue;
}
```
```

**Fig. 5.12** | Function template maximum header.