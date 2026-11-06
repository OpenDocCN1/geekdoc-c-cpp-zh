# ### 3.3.6 Access Specifiers `private` and `public`

The keyword **private** (line 17)

```
```cpp
private:
```
```

is an **access specifier**. Access specifiers are always followed by a colon (`:`). Data member `name`’s declaration (line 18) appears *after* access specifier `private:` to indicate that `name` is accessible *only* to class `Account`’s member functions.⁷ This is known as **data hiding** — the data member `name` is *encapsulated* (hidden) and can be used *only* in class `Account`’s `setName` and `getName` member functions. Most data-member declarations appear after the `private:` access specifier. For the remainder of the text, when we refer to the access specifiers `private` and `public` in the text, we’ll often omit the colon as we did in this sentence.

⁷. Or to “friends” of the class as you’ll see in Section 9.13.

This class also contains the **public** access specifier (line 7)