```
```cpp
template <typename T=int, size_t n=10>
class FixedArray {
    // ...
};
```
```

Here I use the default int type for formal data type T and the default value 10 for non-type parameter n. These are always used when users of the class template do not provide any specifications during instantiation. The same rules apply here as with default values for functions. So if a parameter gets a default value, all other parameters to the right must also get a default value. Specifically, this means that if the formal parameter T has received the default value int, the nontype parameter next to it must also receive a default value.

From the FixedArray class template defined in this way with the two default values, a class can now be instantiated in various ways:

```
```cpp
FixedArray<> vals;                 // FixedArray<int,10>
FixedArray<double> dvals;          // FixedArray<double,10>
FixedArray<char,8> bytes;           // FixedArray<char,8>
FixedArray<100> whatever;            // ⚠ Error!
```
```

From FixedArray<>, the compiler will generate a class with the default values that can hold an int array with 10 values as a property. With FixedArray<double>, however, the formal data type T from the class template is replaced by double, and the compiler generates a double array with 10 (default value) elements as a property. In the case of FixedArray<char,8>, I use both a type for the formal data type and a value for the non-type parameter, resulting in the compiler generating a class that can store a char array with eight elements as a property.

# Alias Template

An instantiation like with FixedArray<100> is not possible because if an argument is omitted during instantiation, all subsequent arguments must also be omitted. There is still a way to use such values with using in angle brackets:

```
```cpp
template <size_t MAX>
using FixedIntArray = FixedArray<int, MAX>;
...
FixedIntArray<100> bigArray01;
```
```

Here, FixedIntArray is a so-called alias template. This allows you to generate a class for an int array, where you can specify the number, like 100 here, in the angle brackets. This class template can now be used with the FixedIntArray alias name. It is important to note that the FixedArray<T, n> class template is still being used. The call is simply made with an alias name to facilitate its use.