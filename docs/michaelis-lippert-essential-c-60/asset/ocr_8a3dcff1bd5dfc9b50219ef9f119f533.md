the lack of localization and other advanced formatting features makes this approach less suitable for general end-user text display.

# Guidelines

**DO** override ToString() whenever useful developer-oriented diagnostic strings can be returned.
**DO** try to keep the string returned from ToString() short.
**DO NOT** return an empty string or null from ToString().
**AVOID** throwing exceptions or making observable side effects (changing the object state) from ToString().
**DO** provide an overloaded ToString(string format) or implement IFormattable if the return value is culture-sensitive or requires formatting (for example, DateTime).
**CONSIDER** returning a unique string from ToString() so as to identify the object instance.

# Overriding GetHashCode()

Overriding GetHashCode() is more complex than overriding ToString(). Even so, you should override GetHashCode() when you are overriding Equals(), and there is a compiler warning to indicate this step is recommended if you don’t. Overriding GetHashCode() is also a good practice when you are using it as a key into a hash table collection (System.Collections.Hashtable and System.Collections.Generic.Dictionary, for example).

The purpose of the hash code is to *efficiently balance a hash table* by generating a number that corresponds to the value of an object. Here are some implementation principles for a good GetHashCode() implementation:

+   - *Required:* Equal objects must have equal hash codes (if a.Equals(b), then a.GetHashCode() == b.GetHashCode()).
+   - *Required:* GetHashCode()’s returns over the life of a particular object should be constant (the same value), even if the object’s data changes. In many cases, you should cache the method return to enforce this constraint.
+   - *Required:* GetHashCode() should not throw any exceptions; GetHashCode() must always successfully return a value.