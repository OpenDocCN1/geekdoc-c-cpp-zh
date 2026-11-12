# Chapter 11

# Namespaces

# **Question 122**    unnamed namespace

What is *unnamed namespace*?

# Solution of Question 122

An *unnamed-namespace* is a namespace without any name with potential to replace usage of static keyword.

An *unnamed-namespace-definition* behaves as if it were replaced by

```
inline namespace unique { /* empty body */ }
using namespace unique;
namespace unique { namespace-body }
```

where inline appears if and only if it appears in the unnamed-namespace-definition, all occurrences of unique in a translation unit are replaced by the same identifier, and this identifier differs from all other identifiers in the entire program.

Although entities in an *unnamed namespace* might have external linkage, they are effectively qualified by a name unique to their translation unit and therefore can never be seen from any other translation unit.

```
namespace
{
    int a;
}

void func()
{

```