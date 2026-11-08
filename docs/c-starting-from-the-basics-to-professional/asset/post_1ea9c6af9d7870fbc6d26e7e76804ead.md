
```cpp
// Prevent copying:
unique_ptr(const unique_ptr&) = delete;
unique_ptr& operator=(const unique_ptr&) = delete;

// Allow moving:
unique_ptr(unique_ptr&& source);
unique_ptr& operator=(unique_ptr&& rhs);
```

To define a move-only type, you always start by deleting its two copy members (like we taught you in Chapter 13). By doing so, you implicitly delete the move members as well (more on this later), so to allow uncopiable objects to be moved you must explicitly define the move members. Often, but not in the case of unique_ptr<>, it would suffice to use = default; to define the two move members and have the compiler generate them for you.

## Extended Use of Moved Objects

An lvalue expression by definition evaluates to a persistent value, which is a value that remains addressable after the execution of the lvalue's parent statement. This is why the compiler normally prefers to copy the value of an lvalue expression. We just told you, however, how you can override this preference with std::move(). That is, you can force the compiler to pass any object to a move constructor or move assignment operator, even if it's not temporary. This raises the question, what happens if you keep using an object after it has been moved? Here's an example (if you want, you can try this in Ex18_04):

```cpp
...
Array<std::string> more_strings{ 2'000 };
strings = std::move(more_strings);        // Move more_strings into strings

std::cout << more_strings[101] << std::endl; // ???
}
```

In this specific case, you of course already know what will happen. After all, you've written the code for the move assignment operator of Array<> yourself. Once moved, an Array<> object will contain an m_elements pointer that is set to nullptr. Any further use of a moved Array<> then would trigger a null pointer dereference, which, as always, is destined to end in the tragic, gruesome death of your program. This example therefore nicely underlines the rationale behind this guideline:

**Caution**  As a rule, you should only move an object if you are absolutely sure it is no longer required. Unless otherwise specified, you're not supposed to keep on using an object that was moved. By default, any extended use of a moved object results in undefined behavior (read: it'll often result in crashes).

This guideline applies to objects of Standard Library types as well. Completely analogous to Arrays, for instance, you must never simply keep using a moved std::vector<>. Doing so could very well end equally badly. You might hope that a moved vector<> is equivalent to an empty one. And while this may be so for some implementations, in general the C++ standard does not specify at all in which state a moved vector<> should be. What is (implicitly) allowed, however, and this is something that not too many developers will know, is this:

> **Tip**  If needed, you can safely revive a `move()`'d `vector<>` by calling its `clear()` member. After calling `clear()`, the `vector<>` is guaranteed to be equivalent to an empty `vector<>` again and thus safe for further use.

In the rare cases where you do want to reuse moved Standard Library objects, you should always check the specification of their move members. When a `std::optional<T>` object that contains a `T` value is moved, for instance, it will still contain a `T` value—that is now moved (we covered `std::optional<>` in Chapter 9). Similar to a `vector<>`, the `optional<>` can safely be reused after calling its `reset()` member. Smart pointers are a scarce exception:

> **Tip**  The Standard Library specification clearly stipulates that you may continue using smart pointers of type `std::unique_ptr<>` and `std::shared_ptr<>` after moving out the raw pointer, and this without first calling `reset()`. For both types, move operations must always set the encapsulated raw pointer to `nullptr`.

## A Barrel of Contradictions

Many find move semantics confusing at first, and understandably so. We hope this section can somewhat spare you from this fate, as it aims to alleviate some of the most common sources of confusion.

### std::move() Does Not Move

Make no mistake, `std::move()` does not move anything. All this function does is turn a given lvalue into an rvalue reference. `std::move()` is effectively nothing more than a type conversion, not at all unlike built-in cast operators `static_cast<>` and `dynamic_cast<>`. In fact, you could almost implement your own version of the function simply like so (somewhat simplified):

```cpp
template <typename T>
T&& move(T&& x) noexcept { return static_cast<T&&>(x); }
```

Clearly, this means nothing. What it does, however, is make a persistent lvalue eligible for binding with the rvalue reference parameter of a move constructor or assignment operator. It’s these member functions that are then supposed to move the members of the former lvalue into another object. `std::move()` only performs a type cast to make the compiler pick the right function overload.

If no function or constructor overload exists with an rvalue reference parameter, an rvalue will happily bind with an lvalue reference instead. That is, you can `move()` all you want; but if there’s no function overload standing ready to receive the resulting rvalue, it’s all in vain.

To demonstrate this, we’ll again start from E18_04.cpp. As you may recall, this latest variant of our running example ended with these statements:

```cpp
...
Array<std::string> more_strings{ 2'000 };
strings = std::move(more_strings);    // Move more_strings into strings
}
```

Obviously, the intent of this final statement is to move the 2,000 strings of `more_strings` into `strings`. And in Ex18_04 this worked flawlessly. But now see what happens if you remove the declaration and definition of the move assignment operator from its `Array<>` template. If you then run the `main()` function of Ex18_04.cpp once more, unaltered, the last line of the output reverts to this:

```text
...
Array of 2000 elements copied
```

It does not matter that you still call `std::move()` in the body of `main()`. If there's no move assignment operator for `Array<>` to accept the rvalue, the copy assignment operator will be used instead. So, always remember, adding `std::move()` is of no consequence if the function or constructor that you are passing a value to has no overload with an rvalue reference parameter!

### An Rvalue Reference Is an Lvalue

To be precise, the name of a named variable with an rvalue reference type is an lvalue. Let's show what we mean by this, as it turns out that many struggle with this idiosyncrasy at first. We'll keep on milking the same example, naturally, so take Ex18_04 once again (make sure it contains the original `Array<>` template where the move assignment operator is still defined) and change the last two lines of the program to the following:

```cpp
...
Array<std::string> more_strings{ 2'000 };
Array<std::string>&& rvalue_ref{ std::move(more_strings) };
strings = rvalue_ref;
}
```

Notwithstanding that the `rvalue_ref` variable clearly has an rvalue reference type, the output of the program will show that the corresponding object is copied:

```text
Array of 1000 elements moved (assignment)
Array of 2000 elements copied
```

Every variable name expression is an lvalue, even if the type of that variable is an rvalue reference type. To move the contents of a named variable, you must therefore always add `std::move()`:

```cpp
strings = std::move(rvalue_ref);
```

While you'd normally not create an rvalue reference in the middle of a block of code like `rvalue_ref` in our latest example, the analogous situation does occur regularly if you define function parameters that are rvalue references. You can find an example of this in the next section.

### Defining Functions Revisited

In this section we’ll study how move semantics has influenced best-practice guidelines for defining new functions, complementing what you saw earlier in Chapter 8. We’ll answer questions such as these: How does move semantics affect the choice between pass-by-reference and pass-by-value? Or, to return an object
