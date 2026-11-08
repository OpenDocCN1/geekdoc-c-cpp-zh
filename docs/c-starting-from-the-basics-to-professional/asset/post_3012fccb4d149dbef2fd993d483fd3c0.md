
This just outputs the values, ten on each line. Thus, you can use a `unique_ptr<T[]>` variable that contains the address of an array just like an array name.

**Tip** It is mostly recommended to use a `vector<T>` container instead of a `unique_ptr<T[]>` because this container type is far more powerful and flexible than the smart pointer. We refer to the end of the previous chapter for a discussion of the various advantages of using vectors.

**Note** The expression `std::make_unique<T>()` creates a variable of type `T` that is value-initialized. For fundamental types (such as `int` and `double`), this means the variable is initialized to zero. Similarly, `std::make_unique<T[]>(n)` creates an array of `n` value-initialized `T` values. This initialization is not always necessary, and may, at times, impact performance (zeroing out memory takes time). In C++20 you can therefore use `std::make_unique_default_init<T>()` or `std::make_unique_default_init<T[]>(n)`. These new creation functions use default initialization instead of value initialization. For fundamental types, default initialization results in indeterminate, uninitialized values (similar to what you get when defining a variable or array variable on the stack without initializing their values).

You can reset the pointer contained in a `unique_ptr<>`, or any type of smart pointer for that matter, by calling its `reset()` function:

```cpp
pvalues.reset();        // Address is nullptr
```

pvalues still exists, but it no longer points to anything. This is a `unique_ptr<double>` object, so because there can be no other unique pointer containing the address of the array, the memory for the array will be released as a result. Naturally, you can check whether a smart pointer contains `nullptr` by explicitly comparing it to `nullptr`, but a smart pointer also conveniently converts to a Boolean value in the same manner as a raw pointer (that is, it converts to false if and only if it contains `nullptr`):

```cpp
if (pvalues)                // Short for:  if (pvalues != nullptr)
    std::cout << "The first value is " << pvalues[0] << std::endl;
```

You create a smart pointer that contains `nullptr` either by using empty braces, `{}`, or simply by omitting the braces:

```cpp
std::unique_ptr<int> my_number;    // Or:  ... my_number{};
                                    // Or:  ... my_number{ nullptr };
if (!my_number)
    std::cout << "my_number points to nothing yet" << std::endl;
```

Creating empty smart pointers would be of little use, were it not that you can always change the value a smart pointer points to. You can do this again using `reset()`:

```cpp
my_number.reset(new int{ 123 });   // my_number points to an integer value 123
my_number.reset(new int{ 42 });    // my_number points to an integer 42
```

Calling `reset()` without arguments is thus equivalent to calling `reset(nullptr)`. When calling `reset()` on a `unique_ptr<T>` object, either with or without arguments, any memory that was previously owned by that smart pointer will be deallocated. So, with the second statement in the previous snippet, the memory containing the integer value 123 gets deallocated, after which the smart pointer takes ownership of the memory slot holding the number 42.

Next to `get()` and `reset()`, a `unique_ptr<>` object also has a member function called `release()`. This function is essentially used to turn the smart pointer back into a dumb raw pointer.

```cpp
int* raw_number = my_number.release(); // my_number points to nullptr after this
...
delete raw_number;                     // The smart pointer no longer does this for you!
```

Take care, though: when calling `release()`, it becomes your responsibility again to apply `delete` or `delete[]` to it. You should therefore use this function only when absolutely necessary, typically when handing over dynamically allocated memory to legacy code. If you do this, always make absolutely sure that this legacy code effectively releases the memory—if not, `get()` is what you should be calling instead!

**Caution** Take care with calling `release()` without capturing the raw pointer that comes out. That is, statements of the following form may very well signal a bug:

```cpp
pvalues.release();
```

Why? Because on its own, this statement introduces a whopping memory leak, of course! You release the smart pointer from the responsibility of deallocating the memory, but since you neglect to capture the raw pointer, there's no way you or anyone else can still apply `delete` or `delete[]` to it anymore. While this may seem obvious now, you'd be surprised how often `release()` is mistakenly called when a `reset()` statement was intended instead:

```cpp
pvalues.reset();         // Not the same as release()!!!
```

The confusion no doubt stems from the fact that the `release()` and `reset()` functions have alliterative names and both functions set the pointer's address to `nullptr`. These similarities notwithstanding, there's of course one rather critical difference: `reset()` deallocates any memory previously owned by the `unique_ptr<>`, whereas `release()` does not.

In general, `release()` is a function you should use only sporadically (typically when interacting with legacy C++ code that does not use smart pointers yet) and with great care not to introduce leaks.

### Using shared_ptr<T> Pointers

You can define a `shared_ptr<T>` object in a similar way to a `unique_ptr<T>` object:

```cpp
std::shared_ptr<double> pdata {new double(999.0)};
```

You can also dereference it to access what it points to or to change the value stored at the address:

```cpp
std::cout << *pdata << std::endl;    // Outputs 999
*pdata = 888.0;
std::cout << *pdata << std::endl;    // Outputs 888
```

Creating a `shared_ptr<T>` object involves a more complicated process than creating a `unique_ptr<T>`, not least because of the need to maintain a reference count. The definition of `pdata` involves one memory allocation for the `double` variable and another allocation relating to the smart pointer object. Allocating memory in the free store is expensive on time. You can make the process more efficient by using the `std::make_shared<T>()` function that is defined in the `<memory>` module to create a smart pointer of type `shared_ptr<T>`:

```cpp
auto pdata{ std::make_shared<double>(999.0) };  // Points to a double variable
```

The type of variable to be created in the free store is specified between the angled brackets. The argument between the parentheses following the function name is used to initialize the `double` variable it creates. In general, there can be any number of arguments to the `make_shared()` function, with the actual number depending on the type of object being created. When you are using `make_shared()` to create objects in the free store, there will often be two or more arguments separated by commas. The `auto` keyword causes the type for `pdata` to be deduced automatically from the object returned by `make_shared<T>()`, so it will be `shared_ptr<double>`.

You can initialize a `shared_ptr<T>` with another when you define it:

```cpp
std::shared_ptr<double> pdata2 {pdata};
```

pdata2 points to the same variable as pdata. You can also assign one `shared_ptr<T>` to another:

```cpp
std::shared_ptr<double> pdata{ std::make_shared<double>(999.0) };
std::shared_ptr<double> pdata2;          // Pointer contains nullptr
pdata2 = pdata;                          // Copy pointer - both point to the same variable
std::cout << *pdata2 << std::endl;       // Outputs 999
```

Of course, copying pdata increases the reference count. Both pointers have to be reset or destroyed for the memory occupied by the `double` variable to be released.

While we may not have explicitly mentioned it in the previous subsection, neither of these operations would be possible with `unique_ptr<>` objects. The compiler would never allow you to create two `unique_ptr<>` objects pointing to the same memory location. With good reason—if it were allowed, both would end up deallocating the same memory, with potentially catastrophic results.

> **Note** Like `std::make_unique<>()`, `std::make_shared<>()` uses value initialization (zero initialization for fundamental types). Mostly that's fine, but in rare occasions you may want to use C++20's `std::make_shared_default_init<>()` instead to improve performance.

Starting with C++20, you can also use `make_shared<T[]>()` to create a `shared_ptr<T[]>` that holds the address of a newly created array in the free store, as follows:

```cpp
auto shared_boole{ std::make_shared<bool[]>(100) };  // A shared array of 100 Booleans
```

- \* `std::make_shared<>()` will typically allocate only a single contiguous memory block that then stores both the `shared_ptr`'s reference count variable and the shared `T` value. This is both faster and more economical in memory usage.
- † Not unless you bypass the compiler's safety checks by using raw pointers, that is, for instance by using `new` or `get()`.
- ‡ Mixing raw pointers and smart pointers is generally a bad idea.
- § `std::shared_ptr<>` gained the ability to manage dynamic arrays already in C++17, but in C++11 you still had to initialize such pointers using their constructor and the `new[]` operator.
