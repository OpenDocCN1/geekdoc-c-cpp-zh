# Returning a Reference

Returning a pointer from a function is useful, but it can be problematic. Pointers can be null, and dereferencing a nullptr generally results in the failure of your program. The solution, as you will surely have guessed from the title of this section, is to return a reference. A reference is an alias for another variable, so we can state the following golden rule for references:

> > **Caution** *Never return a reference to an automatic local variable in a function.*

By returning a reference, you allow a function call to the function to be used on the left of an assignment. In fact, returning a reference from a function is the only way you can enable a function to be used (without dereferencing) on the left of an assignment operation.
Suppose you code a larger() function like this:

```
std::string& larger(std::string& s1, std::string& s2)
{
    return s1 > s2? s1 : s2;    // Return a reference to the larger string
}
```

The return type is "reference to string," and the parameters are references to non-const values. Because you want to return a reference-to-non-const referring to one or other of the arguments, you must not specify the parameters as const.
You could use the function to change the larger of the two arguments, like this:

```
std::string str1 {"abc"};
std::string str2 {"adcf"};
larger(str1, str2) = "def";
```

Because the parameters are not const, you can't use string literals as arguments; the compiler won't allow it. A reference-to-non-const parameter permits the value to be changed, and changing a constant is not something the compiler will knowingly go along with. If you make the parameters const, you can't use a reference-to-non-const as the return type.
We're not going to examine an extended example of using reference return types at this moment, but you can be sure that you'll meet them again before long. As you'll discover, reference return types become essential when you are creating your own data types using classes.

# Returning vs. Output Parameters

You now know two ways a function can pass the outcome it produces back to its caller: it can either return a value or put values into output parameters. In Ex8_08, you encountered the following example of the latter:

```
void find_words(vector<string>& words, const string& str, const string& separators);
```

Another way of declaring this function, however, is as follows:

```
vector<string> find_words(const string& str, const string& separators);
```