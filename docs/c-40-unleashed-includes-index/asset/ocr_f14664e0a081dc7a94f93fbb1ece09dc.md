If you know o ought to be string, use a regular cast instead of an as expression. This will result in an InvalidCastException, which gives you a better clue about what went wrong. In other cases, where you're legitimately using the as keyword, you should expect to see a null check to check the result of the operation.

In an expression context, different ways of dealing with null references exist, as discussed previously. One is the null-coalescing ?? operator, which enables you to provide a default value to replace a null reference; another one is the use of the conditional operator with a null check for the condition:

```
string s = GetStringMaybeNull();
string okay = s ?? "(empty)";
string fine = s != null ? s.ToUpper() : "(empty)";
```

Computer scientist Tony Hoare recently called the introduction of null references in ALGOL (back in 1965) “his billion dollar mistake.” Don’t let them come and get you!

# IndexOutOfRangeException

Another exception in the category of silly bug revealers is IndexOutOfRangeException, which indicates an array is accessed outside its boundaries. “Off-by-one” errors are a typical source of this exception:

```
int[] nums = new[] { 1, 2, 3 };
for (int i = 0; i <= nums.Length; i++)
    nums[i]++;
```

Bounds checks have been a historical source of bugs, which often went unnoticed in the world of native code, causing random program crashes because of memory corruption. Consider yourself lucky that the CLR catches this class of problems using runtime checks (to avoid its memory and type safety), but don’t write such bugs in the first place! Off-by-one errors can be subtle, but with a little bit of extra thought, you should be able to avoid seeing this exception ever again.

# InvalidCastException

Being able to cast an object to an incompatible type would lead to a breach in the type safety of the system, which clearly is to be avoided. InvalidCastException is the CLR’s way to block every such attempt.

Nowadays, after the introduction of generic types, the use of casts should have become much rarer than it used to be. Every time you have to cast an object to a more specific type, ask yourself how you ended up in this situation in the first place. Maybe it has something to do with generics. And if you find yourself performing a type-based switch using is or as, perhaps using object-oriented virtual dispatch facilities is more appropriate.