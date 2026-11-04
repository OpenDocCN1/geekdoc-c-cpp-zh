Fig. 18.1. In this example though, the foreach statement infers element’s type from the array type passed to the method

As in Fig. 18.1, the program of Fig. 18.3 begins by declaring and initializing six-element int array intArray (line 10), seven-element double array doubleArray (line 11) and five-element char array charArray (line 12). Then each array is output by calling DisplayArray (lines 15, 17 and 19)—once with argument intArray, once with argument doubleArray and once with argument charArray.

When the compiler encounters a method call such as line 15, it analyzes the set of methods (both nongeneric and generic) that might match the method call, looking for a method that best matches the call. If there’s no matching method, or if there’s more than one best match, the compiler generates an error.

In the case of line 15, the compiler determines that the best match occurs if the type parameter T in line 23 of method DisplayArray’s declaration is replaced with the type of the elements in the method call’s argument intArray (i.e., int). Then the compiler sets up a call to DisplayArray with int as the type argument for the type parameter T. This is known as the type-inferencing process. The same process is repeated for the calls to method DisplayArray in lines 17 and 19.

![](bbox=[0.2, 0.58, 0.28, 0.68])

# Common Programming Error 18.2

> If the compiler cannot find a single nongeneric or generic method declaration that’s a best match for a method call, or if there are multiple best matches, a compilation error occurs.

For each variable declared with a type parameter, the compiler checks whether the operations performed on the variable are allowed for all types that the type parameter can assume. By default, a type parameter can assume any type, but we’ll show in Section 18.4 that you can restrict this to specific types. The only operation performed on each array element in this example is to output its string representation. Line 27 performs an implicit ToString call on the current array element. Since all objects have a ToString method, the compiler is satisfied that line 27 performs a valid operation for any array element.

By declaring DisplayArray as a generic method in Fig. 18.3, we eliminated the need for the overloaded methods of Fig. 18.1, saving 22 lines of code and creating a reusable method that can output the string representations of the elements in any one-dimensional array, not just arrays of int, double or char elements.

# Value Types vs. Reference Types in Generics

The compiler handles value and reference types differently in generic method calls. When a value-type argument is used for a given type parameter, the compiler generates a version of the method that’s specific to the value type—if one has been generated previously, the compiler reuses that one. So in Fig. 18.3, the compiler generates three versions of method DisplayArray—one each for types int, double and char. If DisplayArray were called with a reference type, the compiler would also generate a single version of the method that’s used by all reference types.

# Explicit Type Arguments

You also can use explicit type arguments to indicate the exact type that should be used to call a generic function. For example, line 15 could be written as

```
DisplayArray<int>(intArray); // pass an int array argument
```