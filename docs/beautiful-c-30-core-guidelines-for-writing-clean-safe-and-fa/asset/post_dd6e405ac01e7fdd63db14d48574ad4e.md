
Why is there a jump from 0x01E1 to 0x0200? Most likely, there was a change in domain after MN_GETHMENU and there was no guarantee that there would be no further additions. It would be easy to identify the domain by looking at the second nibble. Or maybe it was completely arbitrary. We can never know. We cannot capture this information with simple preprocessor definitions.

Enumerated types provide a way of gathering constants together, which make them ideal for identifying, for example, error values, thus creating a specific error abstraction. Rather than declaring:

```cpp
#define OK = 0
#define RECORD_NOT_FOUND = 1
#define TABLE_NOT_FOUND = 2
```

you can define an enumeration instead:

```cpp
enum DB_error {
    OK,
    RECORD_NOT_FOUND,
    TABLE_NOT_FOUND
};
```

The enumerators have the same values as the preprocessor constants since enumerations start at zero by default and increment by one for each enumerator. They are spelled using uppercase letters since they are directly replacing those preprocessor constants. This should be the exception rather than the rule and enumerators should usually be spelled using lowercase letters. This is a matter of style rather than part of the standard: following this style prevents collisions with preprocessor symbols, which are conventionally spelled using uppercase letters.

Unfortunately, the enum keyword does not define a scope, nor does it define an underlying type. This can lead to some interesting problems. Consider an enumeration of two-letter codes for US states. Here is a snippet:

```cpp
enum US_state {
    ...
    MP, // Great quiz question...
    OH,
    OK, // Uh-oh...
    OR,
    PA,
    ...
};
```

Since the braces do not define a scope as normally expected, OK is now an ambiguous identifier. If the enumerations themselves are defined in unrelated scopes this is not a problem. Otherwise, we need to modify the enumerators to disambiguate them. OK is obviously a hugely useful identifier, so it cannot be allowed to exist unadorned. In the pre-C++11 world you would come across enumerators like S_OK, R_OK, E_OK, and so on, leading to somewhat illegible code. Indeed, using a single letter was a luxury afforded only to the biggest players. In the above example you would be far more likely to use DBE_OK or USS_OK. Once you had adorned one enumerator, you felt obliged to adorn all the others, with the result that your code would become scattered with TLAs and underbars prefixing all your enumerators.

Fortunately, although ugly and inconvenient, this hindrance would manifest at compile time in the form of a simple error, easily resolved by uglifying your colliding enumerators a little bit more. The other, rather more insidious problem was that of implicit conversion. Functions could cheerfully return an enumerator like OK, or more likely DBE_OK, and that value could be freely converted to an int. The same was true the other way around: a function could take an int but be passed an enumerator. This leads to interesting bugs where you pass an enumerator from one enumeration and it might be interpreted as an enumerator from another enumeration.

except this will not compile since the left- and right-hand sides of the != sign are of different types, requiring an explicit operator != overload.

There is no guidance on when to use struct or class. Personally, I use class when I have defined other operations on the enumeration. For example, consider a days-of-the-week enumeration:

```cpp
enum class Day {
    monday,
    tuesday,
    wednesday,
    thursday,
    friday,
    saturday,
    sunday
};
```

Perhaps you want to be able to cycle through the days of the week, so you might decide to define a pre-increment operator:

```cpp
constexpr Day operator++(Day& d) {
    switch (d) {
    case Day::monday:   d = Day::tuesday;   break;
    case Day::tuesday:  d = Day::wednesday; break;
    case Day::wednesday: d = Day::thursday;  break;
    case Day::thursday:  d = Day::friday;    break;
    case Day::friday:    d = Day::saturday;  break;
    case Day::saturday:  d = Day::sunday;    break;
    case Day::sunday:    d = Day::monday;    break;
    }
    return d;
}
```

Unfortunately, occasionally it can be unwise to rely on the best efforts of your colleagues and the safest approach is to seek clarification.

## Summary

Prefer class (scoped) enumerations over “plain” (unscoped) enumerations to benefit from a reliable default underlying type and to enable disambiguation of symbols.

Simply adding the keyword class to all your enum declarations is cheap and improves safety by disallowing implicit conversion, while enabling you to improve readability by removing “decoration” from enumerators that was only added to make them unique.

## Postscript

Back in the last decade I arranged for some C++ training for my team to be given by Scott Meyers. This was a pretty big deal for us, and he truly delivered. One of the things that sticks in my mind was that it was the first time I heard someone say enum differently to me. I am English, and I’ve only ever heard this word pronounced to rhyme with “bee-come.” He rhymed it with “resume,” as if he were beginning to say “enumeration” but lost interest after the second syllable.

`std::shared_ptr` object falls out of scope, the object it points to is destroyed. We looked at this where we discussed Core Guideline I.11: "Never transfer ownership by a raw pointer (T*) or reference (T&)." Reference counting is used to do all the book-keeping. The reference is increased when a name is bound to the `std::shared_ptr` object, and decreased if the name falls out of scope.

It is important to remember that names have scope, not objects. Objects have lifetime, or more precisely, storage duration. There are four types of storage duration: static, dynamic, automatic, and thread-local. How many scopes can you name? More than two? In fact, there are six. They are:

- Block
- Namespace
- Class
- Function parameter
- Enumeration
- Template parameter

We shall now look at them all.

## Block scope

Block scope is probably the first one you thought of, although you might not know its name. A block, or compound statement, is a sequence of statements enclosed by braces, as in the following example:

```cpp
if (x > 15) {
    auto y = 200;
    auto z = do_work(y);
    auto gamma = do_more_work(z);
}
```

back in scope at the end of the nested scope, which means its scope is broken up, or discontiguous.

This example is not as healthy as the first one. It is entirely legal, although at best unwise, to reuse names in nested scopes. This is the sort of thing that happens when you paste code from another location and is yet another reason why pasting code is a last resort. The scope and the nested scope take up fewer than a dozen lines that are readable after a fashion, but it is only a matter of time before the code is amended and expanded. Once that happens, the likelihood of the two objects named y becoming mixed up by the author increases.

Some implementations will warn you if you mask a name in this way. Indeed, my implementation of choice introduced this and interfered quite heavily with our no-warnings policy. My stubborn refusal to disable warnings meant that the largest part of the upgrade to this new version of the compiler was fixing all instances of this, uncovering a surprising number of bugs in the process.

## Namespace scope

Like block scope, namespace scope begins after an opening brace. Particularly, it is the brace after the namespace identifier, thus:

```cpp
namespace CG30 { // Scope begins here
```

Any symbol declared before the matching closing brace is visible from its point of declaration. Unlike block scope, it remains visible after the closing brace in all subsequent definitions for the same namespace, for example:

```cpp
namespace CG30 {
    auto y = 76; // Scope of y begins here
} // Scope of y is interrupted here
```
