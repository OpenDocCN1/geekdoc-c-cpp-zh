
However, introducing duplicate definitions for the const and non-const overloads of a member function is considered bad practice. It is a particular instance of what is more generally referred to as code duplication. Because avoiding code duplication is key in making sure your code remains maintainable, we'll contemplate this a bit more before we move on to the final class member template—that for the assignment operator.

### CODE DUPLICATION

Writing the same or similar code more than once is rarely a good idea. Not only is it a waste of time, such so-called duplicated code is undesirable for a number of reasons—most notably because it undermines the maintainability of your code base. Requirements evolve, new insights are gained, and bugs are discovered. So, more often than not, your code will need to be adjusted several times after it is written. Having duplicated code snippets then implies you always have to remember to adjust all copies of that same code. Believe us when we say that this is a maintenance nightmare! The principle of avoiding code duplication is also called the Don't Repeat Yourself (DRY) principle.

Even if the duplicated code is just a few lines, it is often already worthwhile rethinking it. Consider, for instance, the duplicated operator[]() templates we just proposed for the Array<> template. Now imagine that you want to change the type of exception thrown or change the message passed to the exception. Then you have to change it in two places. Not only is this tedious, it is also really easy to forget one of these duplicates—especially if this were code written by someone else, or that you no longer remember the details of. This unfortunately occurs a lot in practice; changes or bug fixes to duplicated code are made in only one or some of the duplicates, while other duplicates live on containing the original now-incorrect version. If each piece of logic appears only once in your code base, this cannot happen!

The good news is that you already know most of the tools you need to battle code duplication. Functions are reusable blocks of computations, templates are instantiated to functions or classes for any number of types, a base class encapsulates all that is common to its derived classes, and so on. All these mechanisms were created precisely to make sure you do not have to repeat yourself!

The traditional approach to eliminate the code duplication between the const and non-const overloads of a member function is to implement the non-const version in terms of its const twin. While this sounds simple enough in principle, the resulting code may, nay will, seem daunting at first. So prepare yourself. For our operator[]() template, for instance, the classical implementation of this idiom looks as follows:

```cpp
template <typename T>
T& Array<T>::operator[](size_t index)
{
    return const_cast<T&>(static_cast<const Array<T>&>(*this)[index]);
}
```

Ouch! We warned you that it would get scary, didn't we? The good news is that C++17 has introduced a little helper template, std::as_const(), that can make this code more bearable:

```cpp
template <typename T>
T& Array<T>::operator[](size_t index)
{
    return const_cast<T&>(std::as_const(*this)[index]);
}
```

Nevertheless, since this is your first encounter with the idiom, let's rewrite this still nonobvious return statement into some smaller steps. That will help us explain what is going on:

```cpp
template <typename T>
T& Array<T>::operator[](size_t index)
{
    Array<T>& nonConstRef = *this;                    // Start from a non-const ref
    const Array<T>& constRef = std::as_const(nonConstRef); // Convert to const ref
    const T& constResult = constRef[index];           // Obtain the const result
    return const_cast<T&>(constResult);               // Convert to non-const result
}
```

Because this template generates non-const member functions, this pointer has a pointer-to-non-const type. So in our case, dereferencing this pointer gives us a reference of type Array<T>&. The first thing we need to do is add const to this type. As of C++17, this can be done using the std::as_const() function template defined in the <utility> module of the Standard Library. Given a value of type T&, instances of this template produce a value of type const T&.

Once we have our reference-to-const, we simply call the overloaded function again with the same set of arguments. In our case, we call the [] operator function again with the same size_t argument, index. The only difference is that this time we call the overloaded function to reference-to-const variable, which means that the const overload of the function—operator[](size_t) const—gets called. If we didn't add const to the type of *this first, we'd simply be calling the same function again, which would trigger infinite recursion.

Because we now call the function on a const object, it typically returns a reference to a const element as well. If it didn't, it would break const correctness. But what we need is a reference to a non-const element. In a final step, we must therefore strip away the constness of the result before returning it from the function. And the only (clean) way to remove const in C++ is by using a const_cast<> (see Chapter 12).

Paraphrasing J. R. R. Tolkien, we propose to call this idiom “const-and-back-again.” You first go from non-const to const (using std::as_const) and then back again to non-const (using a const_cast<>). Note that this idiom is one of the few cases where it is actually recommended to use a const_cast<>. In general, casting away constness is considered bad practice. But eliminating code duplication using the const-and-back-again idiom is a widely accepted exception to this rule.

> **Tip**  Use the const-and-back-again idiom to avoid code duplication between the const and non-const overloads of a member function. In general, it works by implementing the non-const overload of a member in terms of its const counterpart using the following pattern:
>
> ```cpp
> ReturnType MyClass::myFunction(Arguments)
> {
>     return const_cast<ReturnType>(std::as_const(*this).myFunction(Arguments));
> }
> ```

## The Assignment Operator Template

There’s more than one possibility for how the assignment operators could work. The operands must be of the same `Array<T>` type with the same `T`, but this does not prevent them from having different values. You could implement the assignment operators so that the left operands retain the same value for their `m_elements` member whenever possible. That is, if the right operand has fewer elements than the left operand, you could just copy sufficient elements from the right operand to fill parts of the array for the left operand. You could then either leave the excess elements at their original values or set them to the value produced by the default `T` constructor.

To keep it simple, however, we’ll just make a left operand allocate a new `m_elements` array always, even if the previous array would have long enough already to fit a copy of the elements of the right operand. To implement this, the assignment operator functions must release any memory allocated in the destination object and then do what the copy constructors did. To make sure the assignment operator is not `delete[]`ing their own memory, they must first check that the objects are not identical (see Chapter 13). Here’s the definition:

```cpp
template <typename T>
Array<T>& Array<T>::operator=(const Array& rhs)
{
    if (&rhs != this)             // If lhs != rhs
    {
        delete[] m_elements;     // ... do the assignment...
                                  // Release any free store memory

        m_size = rhs.m_size;      // Copy the members of rhs into lhs
        m_elements = new T[m_size];
        for (size_t i = 0; i < m_size; ++i)
            m_elements[i] = rhs.m_elements[i];
    }
    return *this;                  // ... return lhs
}
```

Remember, checking to make sure that the left operand is not identical to the right is essential here; otherwise you’d free the memory for the `m_elements` member of the object pointed to by `this` and then attempt to copy it to itself when it no longer exists! Every assignment operator of this form must start with such a safety check. When the operands are different, you release any free store memory owned by the left operand before creating a copy of the right operand.

> **Note**  Did you notice how we repeated ourselves here? Perhaps take a second look at the assignment operator template if you missed it. The template begins by repeating the logic of the destructor template, followed by that of the copy constructor template. So we are in clear violation of the DRY principle here. But that is not the only thing amiss with this template, as we explain in the upcoming sidebar. The good news, though, is that you can solve both issues in one go using the so-called *copy-and-swap idiom*.
