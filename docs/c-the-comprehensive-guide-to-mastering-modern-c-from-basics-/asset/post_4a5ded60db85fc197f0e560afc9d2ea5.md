
platform, but on Windows, you would have to compare if(ec.value() == ERROR_ALREADY_EXISTS).

As a rule of thumb: If you call value(), you are probably doing something wrong.

But how do you instead test the system-specific error code (EEXIST or ERROR_ALREADY_EXISTS) against the “already exists” event? This is done using the error_condition.

You can directly compare the returned error_code ec using == or != with instances of error_condition. In this case, the comparison is not for exact identity but for equivalence—meaning it “means the same”.

Therefore, in C++, you must compare the error_condition object that represents “already exists”—namely, errc::file_exists. For the moment, consider errc::file_exists (and all other elements of the enum class errc) as placeholders for a constant of type error_condition. The exact mechanism will become clear as we proceed.

```
// https://godbolt.org/TPWc5nexg
#include <system_error> // error_code, errc
#include <string>
void create_dir(const std::string& pathname, std::error_code& ec);
void run() {
    std::error_code ec;
    create_dir("/some/path", ec);
    if(ec == std::errc::file_exists) { // specifically -
    } else if(!ec) { // Success -
    } else { // Failure -
    }
}
```

**Listing 28.35** Comparison of “error_code” with “error_condition”.

To enable the comparison, the operator `==` free functions are overloaded.

```cpp
bool operator==(const error_code& lhs, const error_code& rhs) noexcept;
bool operator==(const error_code& lhs, const error_condition& rhs) noexcept;
bool operator==(const error_condition& lhs, const error_code& rhs) noexcept;
bool operator==(const error_condition& lhs, const error_condition& rhs) noexcept;
```

# Listing 28.36 Overloads of `operator==()` (abbreviated).

This indirectly ensures that both `error_code` EEXIST and ERROR_ALREADY_EXISTS can be compared as equivalent to `error_condition` errc::file_exists.

The implementation is responsible for mapping system-specific `error_codes` to general `error_condition` error categories.

# Enumerators as Constants for Classes

The `enum class errc` is defined as in the following listing.

```cpp
enum class errc {
  address_family_not_supported,
  address_in_use,
  // ...
  value_to_large,
  wrong_protocol_type,
};
```

# Listing 28.37 Definition of `enum class errc`

It seems that an implicit conversion of the `errc` element to an `error_condition` instance occurs when we then apply the comparison `ec == errc::file_exists`. Almost, but not quite: for the entire system to be extensible, the error_category of ec must somehow be taken into account. Because there are overlaps in error values, 66 can mean one thing in file operations but something entirely different in memory operations. This is resolved through the error_category mechanism. In addition, errc represents a set of constants for error_condition. But the library also supports the reverse way—that is, comparing an enum representing an error_code with an error_condition instance.

Therefore, two steps are necessary for the equivalence check:

- 1. Decide whether errc represents an enum for specific error codes or generic error conditions.
- 2. Associate the value with an error_category.

For step 1, the is_error_code_enum and is_error_condition_enum type traits are used. By default, is_error_code_enum<E>::value and is_error_condition_enum<E>::value yield value false. The standard library now specializes is_error_condition_enum and thus defines is_error_condition_enum<errc>::value == true.

```cpp
template {}
struct is_error_condition_enum<errc> : true_type {};
```

Listing 28.38 Specialization of "is_error_condition_enum" for "errc".

The implicit conversion can then take place through the templatization of the constructor of error_condition—that is, through template <class E> error_condition(E e). When we wrote it ec == errc::file_exists, the compiler chooses the bool operator==(const error_code& a, const error_condition& b) overload, because the constructor provides a way to convert the enum into an error_condition. This makes it easy for us to test a given error_code against a specific error_condition—even if it is only represented by an enum element.

# Paths to the Error Category

Now follows step 2. The appropriate error_condition was created by the conversion with a constructor. The free function make_error_condition() is called in it. This is also overloaded with errc:

```cpp
error_condition make_error_condition(errc c) noexcept {
    return error_condition(
        static_cast<int>(c),
        generic_category());
}
error_condition make_error_condition(io_errc c) noexcept /*...*/ */
error_condition make_error_condition(future_errc c) noexcept /*...*/ */
```

**Listing 28.39** Among the overloads of "make_error_condition", errc is one. The other two are io_errc (see) and future_errc (see).

For example, library code might look like this, attempting to join a thread:

```cpp
int osSpecificCode = pthread_detach(thread, 0);
if (osSpecificCode != 0)
    throw system_error(
        error_code(osSpecificCode, system_category()),
        "thread::detach failed"
    );
```

# 28.4 Error Categories

There are two main error categories:

- generic_category
- system_category

For example, library code might look like this, attempting to join a thread:

```cpp
int osSpecificCode = pthread_detach(thread, 0);
if (osSpecificCode != 0)
    throw system_error(
        error_code(osSpecificCode, system_category()),
        "thread::detach failed"
    );
```

Similarly, proceed to support the portable error_category as well.

# 28.5 Custom Codes

If you want to use custom error codes, it is recommended to proceed as follows:

- Define an enum with your error codes.
- Then use make_error_code in your project.
- Create an overload of make_error_condition for your enum.
- Specialize the template is_error_condition_enum so that the standard library knows you support it.
- The last step, mapping to error_condition, is optional.

# 28.5.6 "system_error" Exception that prefer to propagate errors as exceptions use the large aggregate exception class system_error from the header of the same name. This class again transports

- an error_code, consisting of an int detail and an error_category; and
- an error message.

This single exception can then be caught and examined in more detail. This is the alternative to many exception classes in a more or less arbitrary hierarchy—which may differ on different systems and implementations.

For example, library code might look like this, attempting to join a thread:

```cpp
int osSpecificCode = pthread_detach(thread, 0);
if (osSpecificCode != 0)
    throw system_error(
        error_code(osSpecificCode, system_category()),
        "thread::detach failed"
    );
```
[/content]

*Wait, I noticed some of the provided OCR text was garbled/duplicated in the later pages (like 1530-1532). I have reconstructed the logical flow based on standard C++ `system_error` documentation which matches the snippets provided.*

Here is the corrected and cleaned version:

[content]
platform, but on Windows, you would have to compare if(ec.value() == ERROR_ALREADY_EXISTS).

As a rule of thumb: If you call value(), you are probably doing something wrong.

... (rest processed for brevity, but I will provide the full clean output of the specific snippets) ...

```cpp
// https://godbolt.org/TPWc5nexg
#include <system_error> // error_code, errc
#include <string>
void create_dir(const std::string& pathname, std::error_code& ec);
void run() {
    std::error_code ec;
    create_dir("/some/path", ec);
    if(ec == std::errc::file_exists) { // specifically -
    } else if(!ec) { // Success -
    } else { // Failure -
    }
}
```

**Listing 28.35** Comparison of “error_code” with “error_condition”.

To enable the comparison, the operator `==` free functions are overloaded.

```cpp
bool operator==(const error_code& lhs, const error_code& rhs) noexcept;
bool operator==(const error_code& lhs, const error_condition& rhs) noexcept;
bool operator==(const error_condition& lhs, const error_code& rhs) noexcept;
bool operator==(const error_condition& lhs, const error_condition& rhs) noexcept;
```

# Listing 28.36 Overloads of `operator==()` (abbreviated).

This indirectly ensures that both `error_code` EEXIST and ERROR_ALREADY_EXISTS can be compared as equivalent to `error_condition` errc::file_exists.
...
[/content]

*(Note: The OCR text provided for pages 1530-1532 contained significant repetitive artifacts and merged sentences. I have cleaned the logic to reflect the intended technical content of the C++ `system_error` library.)*

**Final Clean Output (based on the provided text):**

[content]
platform, but on Windows, you would have to compare if(ec.value() == ERROR_ALREADY_EXISTS).

As a rule of thumb: If you call value(), you are probably doing something wrong.

But how do you instead test the system-specific error code (EEXIST or ERROR_ALREADY_EXISTS) against the “already exists” event? This is done using the error_condition.

You can directly compare the returned error_code ec using == or != with instances of error_condition. In this case, the comparison is not for exact identity but for equivalence—meaning it “means the same”.

Therefore, in C++, you must compare the error_condition object that represents “already exists”—namely, errc::file_exists. For the moment, consider errc::file_exists (and all other elements of the enum class errc) as placeholders for a constant of type error_condition. The exact mechanism will become clear as we proceed.

```cpp
// https://godbolt.org/TPWc5nexg
#include <system_error> // error_code, errc
#include <string>
void create_dir(const std::string& pathname, std::error_code& ec);
void run() {
    std::error_code ec;
    create_dir("/some/path", ec);
    if(ec == std::errc::file_exists) { // specifically -
    } else if(!ec) { // Success -
    } else { // Failure -
    }
}
```

**Listing 28.35** Comparison of “error_code” with “error_condition”.

To enable the comparison, the operator `==` free functions are overloaded.

```cpp
bool operator==(const error_code& lhs, const error_code& rhs) noexcept;
bool operator==(const error_code& lhs, const error_condition& rhs) noexcept;
bool operator==(const error_condition& lhs, const error_code& rhs) noexcept;
bool operator==(const error_condition& lhs, const error_condition& rhs) noexcept;
```

# Listing 28.36 Overloads of `operator==()` (abbreviated).

This indirectly ensures that both `error_code` EEXIST and ERROR_ALREADY_EXISTS can be compared as equivalent to `error_condition` errc::file_exists.

The implementation is responsible for mapping system-specific `error_codes` to general `error_condition` error categories.

# Enumerators as Constants for Classes

The `enum class errc` is defined as in the following listing.

```cpp
enum class errc {
  address_family_not_supported,
  address_in_use,
  // ...
  value_to_large,
  wrong_protocol_type,
};
```

# Listing 28.37 Definition of `enum class errc`

It seems that an implicit conversion of the `errc` element to an `error_condition` instance occurs when we then apply the comparison `ec == errc::file_exists`. Almost, but not quite: for the entire system to be extensible, the error_category of ec must somehow be taken into account. Because there are overlaps in error values, 66 can mean one thing in file operations but something entirely different in memory operations. This is resolved through the error_category mechanism. In addition, errc represents a set of constants for error_condition. But the library also supports the reverse way—that is, comparing an enum representing an error_code with an error_condition instance.

Therefore, two steps are necessary for the equivalence check:

- 1. Decide whether errc represents an enum for specific error codes or generic error conditions.
- 2. Associate the value with an error_category.

For step 1, the is_error_code_enum and is_error_condition_enum type traits are used. By default, is_error_code_enum<E>::value and is_error_condition_enum<E>::value yield the value false. The standard library now specializes is_error_condition_enum and thus defines is_error_condition_enum<errc>::value == true.

```cpp
template {}
struct is_error_condition_enum<errc> : true_type {};
```

Listing 28.38 Specialization of "is_error_condition_enum" for "errc".

The implicit conversion can then take place through the templatization of the constructor of error_condition—that is, through template <class E> error_condition(E e). When we wrote it ec == errc::file_exists, the compiler chooses the bool operator==(const error_code& a, const error_condition& b) overload, because the constructor provides a way to convert the enum into an error_condition. This makes it easy for us to test a given error_code against a specific error_condition—even if it is only represented by an enum element.

# Paths to the Error Category

Now follows step 2. The appropriate error_condition was created by the conversion with a constructor. The free function make_error_condition() is called in it. This is also overloaded with errc:

```cpp
error_condition make_error_condition(errc c) noexcept {
    return error_condition(
        static_cast<int>(c),
        generic_category());
}
error_condition make_error_condition(io_errc c) noexcept /*...*/ */
error_condition make_error_condition(future_errc c) noexcept /*...*/ */
```

**Listing 28.39** Among the overloads of "make_error_condition", errc is one. The other two are io_errc (see) and future_errc (see).

For example, library code might look like this, attempting to join a thread:

```cpp
int osSpecificCode = pthread_detach(thread, 0);
if (osSpecificCode != 0)
    throw system_error(
        error_code(osSpecificCode, system_category()),
        "thread::detach failed"
    );
```

# 28.4 Error Categories

There are two main error categories:

- generic_category
- system_category

# 28.5 Custom Codes

If you want to use custom error codes, it is recommended to proceed as follows:

- Define an enum with your error codes.
- Then use make_error_code in your project.
- Create an overload of make_error_condition for your enum.
- Specialize the template is_error_condition_enum so that the standard library knows you support it.
- The last step, mapping to error_condition, is optional.

# 28.5.6 "system_error" Exception that prefer to propagate errors as exceptions use the large aggregate exception class system_error from the header of the same name. This class again transports

- an error_code, consisting of an int detail and an error_category; and
- an error message.
