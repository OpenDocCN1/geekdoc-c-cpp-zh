Both the if statement and the null-conditional operator are described in more detail in Chapter 4. While the keyword also appears in Chapter 4 briefly, the full explanation isn’t provided until Chapter 7, which discusses the concept of pattern matching.

# Nullable Value Types

Since a value type refers directly to the actual value, value types cannot innately contain a null because, by definition, they cannot contain references, including references to nothing. Nonetheless we still use the term “dereferencing a value type” when invoking members on the value type. In other words, while not technically correct, using the term “dereferencing” when invoking a member, regardless of whether it is a value type, common.³

# ADVANCED TOPIC

Dereferencing null on Value Types
Technically, value types declared with the nullable modifier are still value types, so even though they have null behavior, under the covers they are not actually null. For, the most part, dereferencing a nullable value type that represents null will not throw a nullable exception. Members like HasValue, ToString(), and even the equality-related members (GetHashCode and Equals()) are all implemented on Nullable<T>, so they won’t throw exceptions when the value is representing null. (Instead, dereferencing a value type throws an InvalidOperationException—not a NullReferenceException—to remind programmers that should check for a value before dereferencing.) However, invoking GetType() when the value represents null does not throw a NullReferenceException. The inconsistency occurs because GetType() is not a virtual method, so Nullable<T> can’t

+   3. Nullable value types were introduced with C# 2.0.