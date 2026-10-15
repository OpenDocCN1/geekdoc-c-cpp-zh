use today: objects. During their research, the team realized that although they were able to use the CLU language to abstract some data representation away from end users of their types, they consistently found themselves having to reveal the inner structure of their data to allow others to intelligently consume it. The result of their consternation was the creation of a language construct called an iterator. (The CLU language offered many insights into what would eventually be popularized as “object-oriented programming.”)

If classes want to support iteration using the foreach loop construct, they must implement the enumerator pattern. As Chapter 14 describes, in C# the foreach loop construct is expanded by the compiler into the while loop construct based on the IEnumerator<T> interface that is retrieved from the IEnumerable<T> interface.

The problem with the enumeration pattern is that it can be cumbersome to implement manually, because it must maintain all the state necessary to describe the current position in the collection. This internal state may be simple for a list collection type class; the index of the current position suffices. In contrast, for data structures that require recursive traversal, such as binary trees, the state can be quite complicated. To mitigate the challenges associated with implementing this pattern, C# 2.0 included a construct that makes it easier for a class to dictate how the foreach loop iterates over its contents.

# Defining an Iterator

Iterators are a means to implement methods of a class, and they are syntactic shortcuts for the more complex enumerator pattern. When the C# compiler encounters an iterator, it expands its contents into CIL code that implements the enumerator pattern. As such, there are no runtime dependencies for implementing iterators. Because the C# compiler handles implementation through CIL code generation, there is no real runtime performance benefit to using iterators. However, there is a substantial programmer productivity gain in choosing iterators over manual implementation of the enumerator pattern. To understand improvement, we first consider how an iterator is defined in code.

# Iterator Syntax

An iterator provides shorthand implementation of iterator interfaces, the combination of the IEnumerable<T> and IEnumerator<T> interfaces. Listing