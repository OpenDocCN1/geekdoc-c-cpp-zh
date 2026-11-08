in the example. Even if this looks different from int, bool, or string, the whole construct is still a single type. The part in the brackets is a parameter to form the overall type. Here vector is the surrounding or main type, and char is the parameter. Together, the two are a “vector of char.”

You could also form a vector<int> and thus obtain a different type. This is important, for example, if the compiler is to decide which functions are available for selection or what the result of an operation is. As I have already mentioned, the compiler calculates with types in the translation phase; the program only calculates on the values at run-time.

One thing that is particularly important here: with parameterized types, what is inside the angle brackets must always be known at compile time. This is only logical as the compiler calculates with types at compile time and the entire construct, consisting of the main type, brackets, and parameters, makes up the type. If you remember this, you will not be surprised when experimenting. For example, there is also the parameterized type std::array<...>, which receives a number as the second template parameter. The number must be a constant or something that the compiler can already calculate, such as 3+4. For example, you can write std::array<int,5> but not int n=5; std::array<int,n>, because n is a variable and as such cannot be part of the type.

> **Note**
> 
> A type must be fixed at compile time.

# Class Template Argument Deduction

You do not always have to specify the arguments of a parameterized type. If you call a constructor, the compiler can infer the types themselves, as in the next example.

```
// https://godbolt.org/z/GbbcnYbqv
std::vector vec { 1, 2, 3 };       // instead of vector<int>
std::tuple tpl { 5, 'x' };          // instead of tuple<int,char>
std::shared_ptr<int> ptr { new int(5) };
std::shared_ptr ptr2 { ptr };       // instead of shared_ptr<int>
```

**Listing 4.18** Since C++17, the compiler determines the type parameters of class templates based on the constructor arguments.

This allows you to keep your code concise and clear in some cases. However, this is not always possible; you will be naming the type parameters often enough yourself.

The class template argument deduction (CTAD) feature has been available since C++17. You can read more about this in Listing 23.3. If you are using an older compiler, write out the parameters of the types.